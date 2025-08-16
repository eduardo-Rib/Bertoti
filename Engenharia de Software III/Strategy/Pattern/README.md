## O Strategy Pattern

O Strategy é um padrão de projeto comportamental que tem como objetivo definir uma família de algoritmos, encapsulá-los e torná-los intercambiáveis. Ele permite que você altere o comportamento de um objeto em tempo de execução sem modificar sua estrutura.

### Quando usar?

- Quando você tem múltiplas variações de um algoritmo (ex.: cálculo de desconto, formas de pagamento, cálculo de frete).

- Para evitar condicionais complexas (if ou switch) para escolher qual algoritmo usar.

- Quando precisa seguir o princípio Open/Closed (aberto para extensão, fechado para modificação).


### Como funciona?

- Interface Strategy: define o método que todas as estratégias devem implementar.

- Concrete Strategies: implementam algoritmos diferentes.

- Context: usa a Strategy e pode trocar a implementação dinamicamente.


### Exemplo:


```java
interface FreteStrategy {
    double calcular(double peso);
}

class Sedex implements FreteStrategy {
    @Override
    public double calcular(double peso) {
        return peso * 10; 
    }
}

class PAC implements FreteStrategy {
    @Override
    public double calcular(double peso) {
        return peso * 5;
    }
}

class CalculadoraFrete {
    private FreteStrategy strategy;

    public CalculadoraFrete(FreteStrategy strategy) {
        this.strategy = strategy;
    }

    public void setStrategy(FreteStrategy strategy) {
        this.strategy = strategy;
    }

    public double calcularFrete(double peso) {
        return strategy.calcular(peso);
    }
}

public class Main {
    public static void main(String[] args) {
        CalculadoraFrete calculadora = new CalculadoraFrete(new Sedex());
        System.out.println("Sedex: R$" + calculadora.calcularFrete(2)); // 2kg

        calculadora.setStrategy(new PAC());
        System.out.println("PAC: R$" + calculadora.calcularFrete(2)); // 2kg
    }
}

```