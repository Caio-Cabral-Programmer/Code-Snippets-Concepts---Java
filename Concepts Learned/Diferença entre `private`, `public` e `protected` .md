# **Diferença entre `private`, `public` e `protected` em Java**

Essas palavras-chave são **modificadores de acesso** que controlam a visibilidade de classes, atributos, métodos e construtores. Vamos entender cada um com exemplos práticos:

## **1. `private` (Privado)**
### **Onde Pode Ser Acessado?**
- **Apenas dentro da própria classe**

### **Exemplo:**
```java
public class ContaBancaria {
    private double saldo; // Só a classe ContaBancaria pode acessar

    public void depositar(double valor) {
        saldo += valor; // OK: método da própria classe
    }
}

// Em outra classe:
ContaBancaria conta = new ContaBancaria();
conta.saldo = 1000; // ERRO: saldo é privado!
```

### **Quando Usar?**
✅ Para **atributos internos** que não devem ser acessados diretamente  
✅ Para **métodos auxiliares** usados apenas dentro da classe  

---

## **2. `public` (Público)**
### **Onde Pode Ser Acessado?**
- **De qualquer lugar** (outras classes, pacotes, projetos)

### **Exemplo:**
```java
public class Calculadora {
    public int somar(int a, int b) {
        return a + b;
    }
}

// Em qualquer outra classe:
Calculadora calc = new Calculadora();
int resultado = calc.somar(2, 3); // OK: método público
```

### **Quando Usar?**
✅ Para **métodos que fazem parte da API** da sua classe  
✅ Para **classes que devem ser instanciadas livremente**  

---

## **3. `protected` (Protegido)**
### **Onde Pode Ser Acessado?**
1. **Dentro da própria classe**
2. **Classes do mesmo pacote**
3. **Subclasses (herança)**, mesmo em pacotes diferentes

### **Exemplo:**
```java
public class Veiculo {
    protected String modelo; // Acessível por subclasses
    
    protected void ligarMotor() {
        System.out.println("Motor ligado");
    }
}

public class Carro extends Veiculo {
    public void exibirModelo() {
        System.out.println(modelo); // OK: subclasse acessando protected
    }
}
```

### **Quando Usar?**
✅ Para **membros que devem ser acessíveis a subclasses**  
✅ Quando quer **limitar o acesso ao mesmo pacote + herança**  

---

## **Tabela Comparativa**
| Modificador | Classe | Pacote | Subclasses | Outros Pacotes |
|------------|--------|--------|------------|----------------|
| `private`  | ✅     | ❌     | ❌         | ❌             |
| `protected`| ✅     | ✅     | ✅         | ❌ (só se for herança) |
| `public`   | ✅     | ✅     | ✅         | ✅             |
| *(sem modificador - default)* | ✅ | ✅ | ❌ | ❌ |

---

## **Exemplo Completo**
```java
package br.com.exemplo;

public class Pessoa {
    private String cpf;          // Só acessível dentro da classe
    protected String nome;       // Acessível por subclasses e mesmo pacote
    public int idade;            // Acessível por todos
    String endereco;             // Default (acessível só no pacote)

    // Construtor público
    public Pessoa(String nome) {
        this.nome = nome;
    }

    // Método privado (uso interno)
    private boolean validarCPF() {
        return cpf.length() == 11;
    }

    // Método protegido
    protected void imprimirNome() {
        System.out.println(nome);
    }
}
```

---

## **Boas Práticas**
1. **Atributos**: Prefira `private` + getters/setters públicos  
2. **Métodos internos**: Use `private`  
3. **Herança**: `protected` para membros que subclasses precisam acessar  
4. **API pública**: `public` apenas para o essencial  

**Dica para iniciantes:** Comece usando `private` para atributos e `public` apenas para métodos que outras classes realmente precisam chamar! 😊  

Quer ver um exemplo de como isso funciona com herança entre pacotes diferentes? Posso te mostrar!
