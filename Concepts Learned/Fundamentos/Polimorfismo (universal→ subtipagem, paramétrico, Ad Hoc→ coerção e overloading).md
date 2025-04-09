# Polimorfismo em Java - Explicação Detalhada para Iniciantes

Polimorfismo é um dos quatro pilares da Programação Orientada a Objetos (junto com encapsulamento, herança e abstração). Vamos explorar todos os tipos de polimorfismo de forma didática.

## O que é Polimorfismo?

Polimorfismo significa "muitas formas" (do grego: poli = muitas, morphos = formas). Em programação, é a capacidade de um objeto se comportar de diferentes maneiras dependendo do contexto.

## Tipos de Polimorfismo

Existem dois grandes grupos de polimorfismo:

1. **Polimorfismo Universal** (mais comum em OOP)
   - Subtipagem (herança)
   - Paramétrico (generics)

2. **Polimorfismo Ad Hoc** (sobrecarga)
   - Coerção (conversão implícita)
   - Overloading (sobrecarga de métodos)

Vamos explorar cada um:

## 1. Polimorfismo por Subtipagem (Herança)

É o mais comum em Java. Ocorre quando uma classe filha pode ser tratada como se fosse da classe pai.

```java
class Animal {
    public void emitirSom() {
        System.out.println("Som genérico de animal");
    }
}

class Cachorro extends Animal {
    @Override
    public void emitirSom() {
        System.out.println("Au au!");
    }
    
    public void abanarRabo() {
        System.out.println("Abanando o rabo!");
    }
}

class Gato extends Animal {
    @Override
    public void emitirSom() {
        System.out.println("Miau!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal meuAnimal; // Tipo Animal
        
        meuAnimal = new Cachorro(); // Polimorfismo - Cachorro é um Animal
        meuAnimal.emitirSom(); // Chama o método de Cachorro
        
        meuAnimal = new Gato(); // Polimorfismo - Gato é um Animal
        meuAnimal.emitirSom(); // Chama o método de Gato
        
        // meuAnimal.abanarRabo(); // Erro! O tipo Animal não conhece este método
    }
}
```

**Características:**
- Usa herança (extends)
- Sobrescrita de métodos (@Override)
- O tipo declarado pode ser superclasse do tipo real
- Só é possível acessar métodos existentes no tipo declarado

## 2. Polimorfismo Paramétrico (Generics)

Permite que classes, interfaces e métodos trabalhem com tipos genéricos.

```java
// Classe genérica
class Caixa<T> {
    private T conteudo;
    
    public void guardar(T conteudo) {
        this.conteudo = conteudo;
    }
    
    public T pegar() {
        return conteudo;
    }
}

public class Main {
    public static void main(String[] args) {
        Caixa<String> caixaDeString = new Caixa<>();
        caixaDeString.guardar("Hello");
        String texto = caixaDeString.pegar();
        
        Caixa<Integer> caixaDeInt = new Caixa<>();
        caixaDeInt.guardar(123);
        int numero = caixaDeInt.pegar();
    }
}
```

**Características:**
- Usa <T> para indicar tipo genérico
- Permite reutilizar código com diferentes tipos
- Garante type-safety em tempo de compilação
- Muito usado em coleções (List<T>, Map<K,V>)

## 3. Polimorfismo por Coerção (Conversão Implícita)

Ocorre quando o Java automaticamente converte um tipo em outro.

```java
public class Main {
    public static void main(String[] args) {
        int inteiro = 10;
        double decimal = inteiro; // Coerção implícita de int para double
        
        System.out.println(decimal); // 10.0
        
        // Outro exemplo:
        long longo = 100;
        float flutuante = longo; // Coerção implícita
    }
}
```

**Características:**
- Conversão automática entre tipos compatíveis
- Sem perda de informação (widening conversion)
- Ocorre em atribuições, passagem de parâmetros, etc.

## 4. Polimorfismo por Overloading (Sobrecarga)

Ocorre quando múltiplos métodos com o mesmo nome, mas assinaturas diferentes, existem na mesma classe.

```java
class Calculadora {
    // Sobrecarga do método somar
    public int somar(int a, int b) {
        return a + b;
    }
    
    public double somar(double a, double b) {
        return a + b;
    }
    
    public String somar(String a, String b) {
        return a + b;
    }
    
    public int somar(int a, int b, int c) {
        return a + b + c;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculadora calc = new Calculadora();
        
        System.out.println(calc.somar(2, 3));          // usa somar(int, int)
        System.out.println(calc.somar(2.5, 3.7));      // usa somar(double, double)
        System.out.println(calc.somar("Olá", " Mundo")); // usa somar(String, String)
        System.out.println(calc.somar(1, 2, 3));       // usa somar(int, int, int)
    }
}
```

**Regras para Overloading:**
- Deve mudar a lista de parâmetros (tipo, quantidade ou ordem)
- Não pode mudar apenas o tipo de retorno
- Pode mudar os modificadores de acesso
- Pode lançar exceções diferentes

## Comparação entre os Tipos

| Tipo de Polimorfismo | Exemplo Java | Quando Ocorre |
|----------------------|--------------|---------------|
| Subtipagem           | @Override    | Herança       |
| Paramétrico          | List<String> | Generics      |
| Coerção              | int → double | Conversões    |
| Overloading          | vários somar() | Mesma classe |

## Exemplo Integrado

Vamos ver todos os tipos juntos:

```java
import java.util.ArrayList;
import java.util.List;

// Polimorfismo paramétrico (generics)
class Zoologico<T extends Animal> {
    private List<T> animais = new ArrayList<>();
    
    public void adicionar(T animal) {
        animais.add(animal);
    }
    
    public void fazerBarulho() {
        for (T animal : animais) {
            animal.emitirSom(); // Polimorfismo por subtipagem
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Zoologico<Animal> zoo = new Zoologico<>();
        
        // Polimorfismo por subtipagem
        zoo.adicionar(new Cachorro());
        zoo.adicionar(new Gato());
        
        zoo.fazerBarulho();
        
        // Polimorfismo por overloading
        Calculadora calc = new Calculadora();
        calc.somar(1, 2);
        calc.somar(1.5, 2.5);
        
        // Polimorfismo por coerção
        double d = 10; // int para double
    }
}
```

## Dicas para Iniciantes

1. **Subtipagem**: Pratique criando hierarquias de classes e usando @Override
2. **Paramétrico**: Comece usando coleções como ArrayList<String>
3. **Coerção**: Observe as conversões automáticas que o Java faz
4. **Overloading**: Crie várias versões de métodos úteis

Lembre-se: o polimorfismo torna seu código mais flexível e reutilizável. Quanto mais você praticar, mais natural vai se tornar o uso desses conceitos!