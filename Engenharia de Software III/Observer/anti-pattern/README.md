## observer-antipattern

### Anti-Pattern: Observer com alto acoplamento (subject conhece concretos)

**O problema**: O sujeito (subject) chama métodos específicos em observadores concretos ou contém lógica condicional para diferentes tipos de observadores. Isso gera alto acoplamento e torna difícil adicionar novos observers sem alterar o subject.

**Quando isso acontece?**

* Desenvolvedores tentam otimizar chamadas ou evitam criar interfaces genéricas.
* Código legado onde alguém "hardcodou" notificações para classes específicas.

**Consequências**

* Difícil manutenção: adicionar novo observer exige editar o subject.
* Viola Open/Closed (modificar para estender).
* Testabilidade reduzida.

**Como usar (exemplo demonstrativo)**

* Compile: `javac *.java`
* Execute: `java MainAnti`

### Arquivos (observer-antipattern)

`SubjectAnti.java` — subject com conhecimento de observers concretos

```java
public class SubjectAnti {
    private ConcreteObserverA a;
    private ConcreteObserverB b;
    private String state;

    public void registerA(ConcreteObserverA a) { this.a = a; }
    public void registerB(ConcreteObserverB b) { this.b = b; }

    public void setState(String newState) {
        this.state = newState;
        // Acoplamento: chama diretamente os métodos dos observadores concretos
        if (a != null) a.receiveA(state);
        if (b != null) b.receiveB(state);
    }
}
```

`ConcreteObserverA.java`

```java
public class ConcreteObserverA {
    public void receiveA(String state) {
        System.out.println("[A] Recebeu: " + state);
    }
}
```

`ConcreteObserverB.java`

```java
public class ConcreteObserverB {
    public void receiveB(String state) {
        System.out.println("[B] Recebeu: " + state);
    }
}
```

`MainAnti.java`

```java
public class MainAnti {
    public static void main(String[] args) {
        SubjectAnti subject = new SubjectAnti();
        ConcreteObserverA a = new ConcreteObserverA();
        ConcreteObserverB b = new ConcreteObserverB();

        subject.registerA(a);
        subject.registerB(b);

        subject.setState("Evento #1");

        // Para adicionar um novo observer C seria preciso editar SubjectAnti -> ruim
    }
}
```

**Melhoria**: usar uma interface `Observer` (como no projeto `observer-pattern`) e fazer o `Subject` manter uma lista genérica — isso remove o acoplamento.