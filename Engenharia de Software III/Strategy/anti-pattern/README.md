## Anti-Pattern do Strategy com Herança

O anti-pattern relacionado ao Strategy usando herança ocorre quando, ao invés de compor comportamentos dinamicamente (como o Strategy propõe), tenta-se resolver o problema com herança.

### Por que isso é ruim?

- Cria uma árvore de herança rígida: cada variação exige uma nova subclasse.

- Dificulta manutenção: se houver muitas combinações de comportamento, o número de subclasses explode.

- Viola o princípio Open/Closed: para adicionar uma nova estratégia, você modifica classes existentes.

- Não permite troca dinâmica: você não consegue mudar a estratégia em tempo de execução, só criando outro objeto.

### Exemplo Simples: Cálculo de Frete com Herança (Anti-Pattern)

```java
class CalculadoraFrete {
    public double calcular(double peso) {
        return peso * 10;
    }
}

class CalculadoraFretePAC extends CalculadoraFrete {
    @Override
    public double calcular(double peso) {
        return peso * 5;
    }
}

class CalculadoraFreteTransportadora extends CalculadoraFrete {
    @Override
    public double calcular(double peso) {
        return peso * 8;
    }
}

public class MainAntiPattern {
    public static void main(String[] args) {
        CalculadoraFrete sedex = new CalculadoraFrete();
        System.out.println("Sedex: R$" + sedex.calcular(2));

        CalculadoraFrete pac = new CalculadoraFretePAC();
        System.out.println("PAC: R$" + pac.calcular(2));

        CalculadoraFrete transportadora = new CalculadoraFreteTransportadora();
        System.out.println("Transportadora: R$" + transportadora.calcular(2));
    }
}
```