# **Programação Orientada a Objetos (POO) em Java - Guia Completo para Iniciantes**

A Programação Orientada a Objetos (POO) é o paradigma fundamental do Java. Vamos explorar seus conceitos essenciais com exemplos práticos e detalhados.

## **1. O que é POO?**
POO é um estilo de programação que organiza o código em "objetos" que representam entidades do mundo real, combinando:
- **Dados** (atributos)
- **Comportamentos** (métodos)

### **Vantagens da POO:**
✔️ Código mais organizado e modular  
✔️ Reutilização através de herança  
✔️ Proteção de dados com encapsulamento  
✔️ Modelagem mais próxima de problemas reais  

---

## **2. Os 4 Pilares da POO em Java**

### **① Encapsulamento**
Protege os dados internos de um objeto, expondo apenas o necessário.

**Como implementar:**
- Atributos como `private`
- Métodos de acesso `public` (getters/setters)

**Exemplo:**
```java
public class ContaBancaria {
    private double saldo;  // Atributo encapsulado

    public void depositar(double valor) {
        if (valor > 0) {
            saldo += valor;
        }
    }

    public double getSaldo() {  // Getter
        return saldo;
    }
}
```

### **② Herança**
Permite criar novas classes baseadas em classes existentes.

**Sintaxe:**
```java
class Animal {  // Superclasse
    void comer() {
        System.out.println("Comendo...");
    }
}

class Cachorro extends Animal {  // Subclasse
    void latir() {
        System.out.println("Au au!");
    }
}
```

**Uso:**
```java
Cachorro meuCao = new Cachorro();
meuCao.comer();  // Herdado de Animal
meuCao.latir();  // Específico de Cachorro
```

### **③ Polimorfismo**
Um objeto pode se comportar de diferentes formas.

**Tipos:**
- **Sobrescrita (Override):** Reescrever método da superclasse
- **Sobrecarga (Overload):** Múltiplos métodos com mesmo nome

**Exemplo de Sobrescrita:**
```java
class Animal {
    void emitirSom() {
        System.out.println("Som genérico");
    }
}

class Gato extends Animal {
    @Override
    void emitirSom() {
        System.out.println("Miau!");
    }
}
```

### **④ Abstração**
Simplifica a complexidade focando no essencial.

**Implementado via:**
- Classes abstratas (`abstract class`)
- Interfaces

**Exemplo com Classe Abstrata:**
```java
abstract class Forma {
    abstract double calcularArea();  // Método sem implementação

    void mostrarTipo() {
        System.out.println("Eu sou uma forma");
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

---

## **3. Classes e Objetos - Diferença Fundamental**

| **Classe** | **Objeto** |
|------------|------------|
| Modelo/planta (definição) | Instância concreta |
| `class Carro { ... }` | `Carro meuCarro = new Carro();` |
| Existe apenas no código | Existe em memória durante a execução |

**Exemplo Prático:**
```java
// Definição da classe
class Lampada {
    boolean ligada;
    
    void acender() {
        ligada = true;
    }
}

// Criando objetos
Lampada sala = new Lampada();
Lampada cozinha = new Lampada();

sala.acender();  // Altera apenas o objeto 'sala'
```

---

## **4. Construtores em Java**
Métodos especiais que inicializam objetos.

**Características:**
- Mesmo nome da classe
- Sem tipo de retorno
- Pode ter parâmetros

**Exemplo:**
```java
class Pessoa {
    String nome;
    int idade;

    // Construtor
    public Pessoa(String nome, int idade) {
        this.nome = nome;
        this.idade = idade;
    }
}

// Uso:
Pessoa p = new Pessoa("João", 30);
```

---

## **5. Interfaces em Java**
Contratos que definem **o que** uma classe deve fazer, sem dizer **como**.

**Exemplo:**
```java
interface Autenticavel {
    boolean autenticar(String senha);
}

class Usuario implements Autenticavel {
    private String senha;

    @Override
    public boolean autenticar(String senha) {
        return this.senha.equals(senha);
    }
}
```

**Principais usos:**
- Definir comportamentos comuns
- Permitir múltiplas "heranças" (Java não tem herança múltipla de classes)
- Criar sistemas fracamente acoplados

---

## **6. Pacotes (Packages)**
Organizam classes relacionadas.

**Estrutura típica:**
```
src/
└── com/
    └── empresa/
        ├── model/
        │   ├── Produto.java
        │   └── Cliente.java
        ├── service/
        └── util/
```

**Declaração:**
```java
package com.empresa.model;

public class Produto {
    // ...
}
```

---

## **7. Princípios SOLID (POO Avançada)**
1. **S** - Single Responsibility (Uma classe, uma responsabilidade)
2. **O** - Open/Closed (Aberto para extensão, fechado para modificação)
3. **L** - Liskov Substitution (Subclasses devem substituir superclasses)
4. **I** - Interface Segregation (Muitas interfaces específicas)
5. **D** - Dependency Inversion (Depender de abstrações, não implementações)

---

## **Exemplo Completo de POO em Java**
```java
// Abstração
abstract class Veiculo {
    private String modelo;
    
    public Veiculo(String modelo) {
        this.modelo = modelo;
    }
    
    abstract void mover();
}

// Encapsulamento + Herança
class Carro extends Veiculo {
    private int velocidade;
    
    public Carro(String modelo) {
        super(modelo);
    }
    
    // Polimorfismo (sobrescrita)
    @Override
    void mover() {
        System.out.println("Carro andando...");
        velocidade = 40;
    }
    
    public int getVelocidade() {
        return velocidade;
    }
}

// Interface
interface Radio {
    void ligarRadio();
}

// Herança múltipla via interface
class CarroLuxo extends Carro implements Radio {
    public CarroLuxo(String modelo) {
        super(modelo);
    }
    
    @Override
    public void ligarRadio() {
        System.out.println("Rádio premium ligado!");
    }
}

// Uso
public class Main {
    public static void main(String[] args) {
        CarroLuxo meuCarro = new CarroLuxo("Ferrari");
        meuCarro.mover();
        meuCarro.ligarRadio();
        System.out.println("Velocidade: " + meuCarro.getVelocidade() + "km/h");
    }
}
```

## **Próximos Passos para Aprender POO em Java**
1. Pratique criando classes simples (ContaBancaria, Produto, etc.)
2. Implemente relações de herança (Animal -> Cachorro, Gato)
3. Experimente polimorfismo com métodos sobrecarregados/sobrescritos
4. Explore interfaces criando sistemas modulares

A POO é essencial para se tornar um desenvolvedor Java eficiente. Quanto mais você praticar esses conceitos, mais natural eles se tornarão! 🚀