# **Pilares da POO em Java: Herança, Polimorfismo, Encapsulamento e Abstração**

Vamos explorar os quatro conceitos fundamentais da Programação Orientada a Objetos (POO) em Java, com exemplos práticos para iniciantes.

## 1. **Herança (Inheritance)**
### O que é?
Mecanismo onde uma classe **herda** atributos e métodos de outra classe, promovendo reuso de código.

### Como funciona?
- **Superclasse (pai)**: Classe que é herdada
- **Subclasse (filha)**: Classe que herda

### Exemplo Prático
```java
// Superclasse
class Animal {
    String nome;
    
    void comer() {
        System.out.println(nome + " está comendo.");
    }
}

// Subclasse
class Cachorro extends Animal {  // 'extends' indica herança
    void latir() {
        System.out.println(nome + " está latindo!");
    }
}

// Uso
public class Main {
    public static void main(String[] args) {
        Cachorro meuCao = new Cachorro();
        meuCao.nome = "Rex";
        meuCao.comer();  // Método herdado
        meuCao.latir();  // Método próprio
    }
}
```

### Características
✔ **Reutilização de código**  
✔ **Relacionamento "é-um"** (um Cachorro **é um** Animal)  
✔ **Herança única** em Java (uma classe só herda de uma superclasse)  

---

## 2. **Polimorfismo (Polymorphism)**
### O que é?
Capacidade de um objeto ser referenciado de múltiplas formas ("muitas formas").

### Tipos:
#### a) Polimorfismo de Sobrescrita (Override)
```java
class Animal {
    void emitirSom() {
        System.out.println("Som genérico");
    }
}

class Gato extends Animal {
    @Override  // Anotação opcional
    void emitirSom() {
        System.out.println("Miau!");
    }
}

// Teste
Animal meuAnimal = new Gato();
meuAnimal.emitirSom();  // Saída: "Miau!" (chama a versão do Gato)
```

#### b) Polimorfismo de Sobrecarga (Overload)
```java
class Calculadora {
    int somar(int a, int b) {
        return a + b;
    }
    
    // Mesmo nome, parâmetros diferentes
    double somar(double a, double b) {
        return a + b;
    }
}
```

### Quando usar?
✔ Quando queremos **comportamentos diferentes** para classes relacionadas  
✔ Para implementar **interfaces comuns** de formas distintas  

---

## 3. **Encapsulamento (Encapsulation)**
### O que é?
Proteção dos dados internos de um objeto, expondo apenas o necessário.

### Como implementar?
- **Modificadores de acesso**:
  - `private`: Só acessível na própria classe
  - `protected`: Acessível na classe e subclasses
  - `public`: Acessível em qualquer lugar

### Exemplo
```java
class ContaBancaria {
    private double saldo;  // Atributo privado
    
    // Métodos públicos para acesso controlado
    public void depositar(double valor) {
        if (valor > 0) {
            saldo += valor;
        }
    }
    
    public double getSaldo() {
        return saldo;
    }
}

// Uso
ContaBancaria conta = new ContaBancaria();
conta.depositar(1000);
System.out.println(conta.getSaldo());  // Acesso seguro
```

### Benefícios
✔ **Proteção de dados** (evita acesso indevido)  
✔ **Flexibilidade** (pode mudar implementação sem afetar outros códigos)  
✔ **Controle de validações** (como no exemplo do depósito)  

---

## 4. **Abstração (Abstraction)**
### O que é?
Focar no **essencial** e esconder detalhes complexos.

### Implementação:
#### a) Classes Abstratas
```java
abstract class Forma {
    abstract double calcularArea();  // Método sem implementação
    
    void imprimir() {
        System.out.println("Área: " + calcularArea());
    }
}

class Circulo extends Forma {
    double raio;
    
    @Override
    double calcularArea() {
        return Math.PI * raio * raio;
    }
}
```

#### b) Interfaces
```java
interface Autenticavel {
    boolean autenticar(String senha);  // Método abstrato
}

class Usuario implements Autenticavel {
    @Override
    public boolean autenticar(String senha) {
        return senha.equals("1234");
    }
}
```

### Quando usar?
✔ Quando queremos **definir um contrato** (o "qué" sem o "como")  
✔ Para **desacoplar** implementações  

---

## **Comparação entre os Conceitos**

| Conceito       | Objetivo Principal               | Exemplo Comum                |
|----------------|----------------------------------|------------------------------|
| **Herança**    | Reutilizar código                | `Cachorro extends Animal`    |
| **Polimorfismo**| Objetos se comportarem de múltiplas formas | `Animal a = new Cachorro()` |
| **Encapsulamento**| Proteger dados internos       | Atributos `private` com getters |
| **Abstração**  | Esconder complexidade            | Classes `abstract` e `interface` |

---

## **Exemplo Integrado**
```java
// Abstração (Interface)
interface Veiculo {
    void acelerar();
}

// Encapsulamento
class Carro implements Veiculo {
    private int velocidade;
    
    @Override
    public void acelerar() {
        velocidade += 10;
    }
    
    public int getVelocidade() {
        return velocidade;
    }
}

// Herança + Polimorfismo
class CarroEsportivo extends Carro {
    @Override
    public void acelerar() {
        velocidade += 25;  // Comportamento diferente
    }
}

// Teste
public class Main {
    public static void main(String[] args) {
        Veiculo meuVeiculo = new CarroEsportivo();  // Polimorfismo
        meuVeiculo.acelerar();
        System.out.println(((Carro)meuVeiculo).getVelocidade());  // Saída: 25
    }
}
```

---

## **Dicas para Iniciantes**
1. Comece com **encapsulamento** (getters/setters)
2. Pratique **herança** em hierarquias simples (ex: Animal -> Cachorro)
3. Use **polimorfismo** com métodos sobrescritos
4. Explore **abstração** com interfaces antes de classes abstratas

Esses conceitos são a base da POO em Java. Pratique criando pequenos projetos para consolidar o aprendizado! 😊