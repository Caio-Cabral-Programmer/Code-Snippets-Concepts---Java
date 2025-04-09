# Enums em Java (Explicação para Iniciantes)

Vamos explorar o conceito de `enum` em Java, que é um tipo especial de classe usado para representar um conjunto de constantes fixas.

## O que é um Enum?

Enum (abreviação de "enumeration", ou enumeração) é um tipo de dado especial que permite definir um conjunto de constantes nomeadas. Ele foi introduzido no Java 5 para substituir o uso de constantes numéricas ou strings, tornando o código mais seguro e legível.

### Problema que o enum resolve (antes do enum):

Antigamente, usávamos constantes assim:
```java
public class DiaSemana {
    public static final int SEGUNDA = 1;
    public static final int TERCA = 2;
    // ...
    public static final int DOMINGO = 7;
}
```

Isso tinha problemas:
- Não era type-safe (podíamos passar qualquer inteiro)
- Não tinha namespaces (precisava usar prefixos)
- Não podia adicionar comportamentos

## Sintaxe Básica

A forma mais simples de declarar um enum:

```java
public enum DiaDaSemana {
    SEGUNDA, TERCA, QUARTA, QUINTA, SEXTA, SABADO, DOMINGO
}
```

## Características Principais

1. **São constantes**: Os valores do enum são instâncias imutáveis da classe enum
2. **São singleton**: Cada constante existe apenas uma vez na JVM
3. **Podem ter métodos e campos**: Como qualquer classe
4. **Podem implementar interfaces**: Mas não podem estender classes
5. **São type-safe**: Só aceitam os valores definidos

## Como Usar um Enum

### Declaração e uso simples:
```java
public enum NivelPrioridade {
    BAIXA, MEDIA, ALTA, URGENTE
}

public class Tarefa {
    private NivelPrioridade prioridade;
    
    public void setPrioridade(NivelPrioridade prioridade) {
        this.prioridade = prioridade;
    }
}

// Usando:
Tarefa tarefa = new Tarefa();
tarefa.setPrioridade(NivelPrioridade.ALTA);  // Correto
// tarefa.setPrioridade("ALTA");             // Erro! Type-safe
```

## Métodos Úteis dos Enums

Todo enum tem automaticamente estes métodos:

1. **values()**: Retorna um array com todas as constantes
   ```java
   for (DiaDaSemana dia : DiaDaSemana.values()) {
       System.out.println(dia);
   }
   ```

2. **valueOf()**: Converte uma string para a constante enum
   ```java
   DiaDaSemana dia = DiaDaSemana.valueOf("SEGUNDA"); // Retorna SEGUNDA
   // DiaDaSemana.valueOf("segunda"); // Lança IllegalArgumentException
   ```

3. **ordinal()**: Retorna a posição da constante na declaração (começa em 0)
   ```java
   System.out.println(DiaDaSemana.SEGUNDA.ordinal()); // 0
   System.out.println(DiaDaSemana.TERCA.ordinal());   // 1
   ```

## Enums com Construtores e Métodos

Enums podem ter construtores, campos e métodos como classes normais:

```java
public enum Planetas {
    MERCURIO(3.303e+23, 2.4397e6),
    VENUS(4.869e+24, 6.0518e6),
    TERRA(5.976e+24, 6.37814e6);
    
    private final double massa;   // em quilogramas
    private final double raio;    // em metros
    
    // Construtor do enum (sempre private)
    Planetas(double massa, double raio) {
        this.massa = massa;
        this.raio = raio;
    }
    
    public double getMassa() { return massa; }
    public double getRaio() { return raio; }
    
    // Método que calcula a gravidade na superfície
    public double gravidadeSuperficie() {
        final double G = 6.67300E-11; // constante gravitacional
        return G * massa / (raio * raio);
    }
}

// Usando:
public class TestePlanetas {
    public static void main(String[] args) {
        System.out.println("Gravidade na Terra: " + 
            Planetas.TERRA.gravidadeSuperficie() + " m/s²");
    }
}
```

## Enums com Comportamentos Específicos

Podemos dar comportamentos diferentes para cada constante:

```java
public enum OperacaoMatematica {
    SOMA {
        public double calcular(double x, double y) { return x + y; }
    },
    SUBTRACAO {
        public double calcular(double x, double y) { return x - y; }
    },
    MULTIPLICACAO {
        public double calcular(double x, double y) { return x * y; }
    },
    DIVISAO {
        public double calcular(double x, double y) { return x / y; }
    };
    
    public abstract double calcular(double x, double y);
}

// Usando:
public class Calculadora {
    public static void main(String[] args) {
        double resultado = OperacaoMatematica.SOMA.calcular(5, 3);
        System.out.println("5 + 3 = " + resultado);
    }
}
```

## Quando Usar Enums?

Use enums quando:
- Você tem um conjunto fixo de constantes relacionadas
- Você precisa de segurança de tipos (type-safety)
- Você quer associar comportamentos às constantes
- Você precisa usar as constantes em estruturas como switch-case

## Exemplo com Switch-Case

Enums funcionam muito bem com switch:

```java
public enum EstadoProcesso {
    NOVO, EXECUTANDO, AGUARDANDO, FINALIZADO, CANCELADO
}

public class Processo {
    private EstadoProcesso estado;
    
    public void avancarEstado() {
        switch (estado) {
            case NOVO:
                estado = EstadoProcesso.EXECUTANDO;
                break;
            case EXECUTANDO:
                estado = EstadoProcesso.AGUARDANDO;
                break;
            case AGUARDANDO:
                estado = EstadoProcesso.FINALIZADO;
                break;
            default:
                System.out.println("Processo já finalizado ou cancelado");
        }
    }
}
```

## Boas Práticas com Enums

1. Use nomes em MAIÚSCULAS para as constantes (convenção Java)
2. Coloque os enums em arquivos separados quando forem complexos
3. Use enums em vez de constantes numéricas ou strings sempre que possível
4. Considere usar enums para implementar o padrão Singleton

## Exemplo de Singleton com Enum

A forma mais segura de implementar Singleton em Java:

```java
public enum DatabaseConnection {
    INSTANCE;
    
    public void connect() {
        System.out.println("Conectando ao banco de dados...");
    }
    
    public void disconnect() {
        System.out.println("Desconectando do banco de dados...");
    }
}

// Usando:
public class Aplicacao {
    public static void main(String[] args) {
        DatabaseConnection.INSTANCE.connect();
        // ...
        DatabaseConnection.INSTANCE.disconnect();
    }
}
```

## Resumo

- Enums são classes especiais que representam conjuntos fixos de constantes
- São type-safe, mais seguros e legíveis que constantes numéricas/strings
- Podem ter construtores, métodos e campos como classes normais
- São implicitamente `final` e seus construtores são privados
- Todos enums estendem `java.lang.Enum`
- São a melhor opção para representar conjuntos fixos de valores relacionados

Praticar com enums é a melhor maneira de aprender. Tente criar seus próprios enums para situações como:
- Status de pedidos (ABERTO, PROCESSANDO, ENVIADO, ENTREGUE)
- Cores primárias
- Direções (NORTE, SUL, LESTE, OESTE)
- Tipos de usuário (ADMIN, EDITOR, VISITANTE)
