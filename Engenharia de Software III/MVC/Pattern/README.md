## mvc-pattern

### MVC (Model-View-Controller) — Padrão

O MVC separa responsabilidades:

* **Model**: lógica e dados da aplicação.
* **View**: apresentação (UI).
* **Controller**: recebe entrada do usuário e atualiza Model/View.

**Quando usar?**

* Aplicações com UI (web, desktop) onde separação de responsabilidades traz clareza.
* Projetos que precisam ser testáveis e expansíveis.

**Como funciona?**

* O Controller altera o Model; o Model notifica a View (observer/listener), e a View atualiza a apresentação.

**Como usar**

* Compile: `javac *.java`
* Execute: `java MainMVC`

**Exemplo**: contador simples (incrementar/decrementar). Model notifica as Views via `ModelListener`.

### Arquivos (mvc-pattern)

`CounterModel.java`

```java
import java.util.ArrayList;
import java.util.List;

public class CounterModel {
    private int count = 0;
    private final List<ModelListener> listeners = new ArrayList<>();

    public int getCount() { return count; }

    public void increment() {
        count++;
        notifyListeners();
    }

    public void decrement() {
        count--;
        notifyListeners();
    }

    public void addListener(ModelListener l) { listeners.add(l); }
    public void removeListener(ModelListener l) { listeners.remove(l); }

    private void notifyListeners() {
        for (ModelListener l : listeners) l.onModelChanged(count);
    }
}
```

`ModelListener.java`

```java
public interface ModelListener {
    void onModelChanged(int newValue);
}
```

`CounterView.java`

```java
public class CounterView implements ModelListener {
    private final CounterController controller;

    public CounterView(CounterController controller) {
        this.controller = controller;
    }

    @Override
    public void onModelChanged(int newValue) {
        System.out.println("[VIEW] Valor atual: " + newValue);
    }

    // Simula interação do usuário
    public void pressIncrement() { controller.increment(); }
    public void pressDecrement() { controller.decrement(); }
}
```

`CounterController.java`

```java
public class CounterController {
    private final CounterModel model;

    public CounterController(CounterModel model) { this.model = model; }

    public void increment() { model.increment(); }
    public void decrement() { model.decrement(); }
}
```

`MainMVC.java`

```java
public class MainMVC {
    public static void main(String[] args) throws InterruptedException {
        CounterModel model = new CounterModel();
        CounterController controller = new CounterController(model);
        CounterView view = new CounterView(controller);

        model.addListener(view);

        // Simula ações do usuário
        view.pressIncrement(); // +1
        Thread.sleep(200);
        view.pressIncrement(); // +1
        Thread.sleep(200);
        view.pressDecrement(); // -1
    }
}