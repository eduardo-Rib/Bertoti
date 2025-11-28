## observer-pattern

### Observer Pattern

O Observer é um padrão comportamental que define uma dependência um-para-muitos entre objetos. Quando o objeto observado muda de estado, todos os seus dependentes são notificados automaticamente.

**Quando usar?**

* Quando alterações no estado de um objeto devem refletir em vários outros objetos.
* Para evitar acoplamento rígido entre o "sujeito" (subject) e os interessados (observers).
* Quando você quer permitir que objetos se inscrevam (subscribe) para receber atualizações.

**Como funciona?**

* Subject (ou Observable): mantém uma lista de observers e fornece métodos para adicionar/remover/notify.
* Observer: interface que define o método `update(...)` que será chamado pelo Subject.
* ConcreteObservers: implementam a interface Observer.
* ConcreteSubject: armazena estado e chama `notifyObservers()` quando o estado muda.

**Como usar**

* Compile: `javac *.java`
* Execute: `java Main`

**Exemplo**: um `ConcreteSubject` que representa um preço de produto. Observers (ConsoleObserver e LogObserver) reagem quando o preço muda.

### Arquivos (observer-pattern)

`Subject.java`

```java
import java.util.ArrayList;
import java.util.List;

public class Subject {
    private final List<Observer> observers = new ArrayList<>();
    private String state;

    public void attach(Observer o) { observers.add(o); }
    public void detach(Observer o) { observers.remove(o); }

    public void setState(String newState) {
        this.state = newState;
        notifyObservers();
    }

    public String getState() { return state; }

    private void notifyObservers() {
        for (Observer o : observers) {
            o.update(this);
        }
    }
}
```

`Observer.java`

```java
public interface Observer {
    void update(Subject subject);
}
```

`ConsoleObserver.java`

```java
public class ConsoleObserver implements Observer {
    private final String name;

    public ConsoleObserver(String name) { this.name = name; }

    @Override
    public void update(Subject subject) {
        System.out.println("[ConsoleObserver - " + name + "] Notified. New state: " + subject.getState());
    }
}
```

`LogObserver.java`

```java
public class LogObserver implements Observer {
    @Override
    public void update(Subject subject) {
        // exemplo simples: apenas print, mas poderia gravar em arquivo
        System.out.println("[LogObserver] Gravando log: estado alterado para -> " + subject.getState());
    }
}
```

`Main.java`

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Subject subject = new Subject();

        ConsoleObserver obs1 = new ConsoleObserver("A");
        ConsoleObserver obs2 = new ConsoleObserver("B");
        LogObserver log = new LogObserver();

        subject.attach(obs1);
        subject.attach(log);

        subject.setState("Preço: R$50");

        // remover um observer em runtime
        subject.detach(obs1);
        subject.attach(obs2);

        subject.setState("Preço: R$45");
    }
}
```