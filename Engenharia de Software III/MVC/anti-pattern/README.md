## mvc-antipattern

### Anti-Pattern MVC: God Object / Massive View-Controller

**O problema**: lógica de negócios, apresentação e controle ficam juntos em uma mesma classe, gerando um "God Object" que faz tudo. Esse anti-padrão torna manutenção, testes e evolução difíceis.

**Consequências**

* Código difícil de testar.
* Difícil separar responsabilidades.
* Alterar a UI pode quebrar a lógica de negócios.

**Como usar (exemplo demonstrativo)**

* Compile: `javac *.java`
* Execute: `java BadApp`

### Arquivos (mvc-antipattern)

`BadApp.java`

```java
import java.util.Scanner;

public class BadApp {
    private int count = 0; // model

    public void run() {
        Scanner sc = new Scanner(System.in);
        System.out.println("Aplicativo simples (anti-pattern). Comandos: +, -, q");
        while (true) {
            System.out.print("Comando: ");
            String cmd = sc.nextLine();
            if (cmd.equals("+")) {
                // mistura lógica de negócio e apresentação no mesmo local
                count++;
                System.out.println("Novo valor: " + count);
            } else if (cmd.equals("-")) {
                count--;
                System.out.println("Novo valor: " + count);
            } else if (cmd.equals("q")) {
                System.out.println("Saindo...");
                break;
            } else {
                System.out.println("Comando inválido");
            }
        }
        sc.close();
    }

    public static void main(String[] args) {
        new BadApp().run();
    }
}
```

**Melhoria**: separar `BadApp` em `Model`, `View` e `Controller` como no `mvc-pattern`.