### **O que são Variáveis em Java? (Explicação para Iniciantes)**  

Em programação, uma **variável** é um **espaço na memória** que armazena um valor (dado) que pode ser alterado durante a execução do programa.  

Pense em uma variável como uma **caixa** onde você guarda algo:  
- Cada caixa tem um **nome** (identificador da variável).  
- Cada caixa tem um **tipo** (define que tipo de dado ela pode guardar).  
- Você pode **colocar, ler ou modificar** o conteúdo da caixa.  

---

### **1. Como Declarar uma Variável em Java?**  
Sintaxe básica:  
```java
tipo nomeDaVariavel = valor;
```
Exemplo:  
```java
int idade = 20;          // Variável do tipo 'int' (número inteiro)
double preco = 19.99;    // Variável do tipo 'double' (número decimal)
String nome = "Maria";   // Variável do tipo 'String' (texto)
boolean ativo = true;    // Variável do tipo 'boolean' (verdadeiro/falso)
```

---

### **2. Tipos de Variáveis em Java**  
Java tem dois grandes grupos de variáveis:  

#### **a) Variáveis Primitivas**  
Armazenam valores diretamente (não são objetos). Os principais tipos são:  

| Tipo      | Exemplo       | Descrição                          |
|-----------|--------------|-----------------------------------|
| `int`     | `int x = 10;` | Números inteiros (ex: 10, -5)      |
| `double`  | `double y = 3.14;` | Números decimais (ex: 2.5, -1.75) |
| `char`    | `char letra = 'A';` | Um único caractere (ex: 'A', '7') |
| `boolean` | `boolean ligado = true;` | `true` ou `false` (verdadeiro/falso) |

#### **b) Variáveis de Referência (Objetos)**  
Armazenam a **referência** (endereço) de um objeto na memória. Exemplos:  

```java
String texto = "Olá, mundo!";  // String é um objeto
Scanner entrada = new Scanner(System.in); // Scanner é um objeto
```

---

### **3. Regras para Nomear Variáveis**  
- Devem começar com **letra, `_` ou `$`** (não pode número no início).  
- Não podem ser **palavras reservadas** (`if`, `for`, `class`, etc.).  
- Java é **case-sensitive** (`idade` ≠ `Idade`).  
- Use nomes descritivos (`salario` em vez de `s`).  

Exemplos válidos:  
```java
int idadeUsuario;
double _valorTotal;
String $nomeDaEmpresa;
```

Exemplos inválidos:  
```java
int 2alunos;       // Errado! Não pode começar com número
double salário;    // Cuidado! Evite acentos (use "salario")
String class;      // Errado! "class" é palavra reservada
```

---

### **4. Para que Servem as Variáveis?**  
- **Armazenar dados temporários** (como entrada do usuário).  
- **Facilitar cálculos** (ex: `total = preco * quantidade`).  
- **Controlar fluxo do programa** (ex: `if (idade >= 18)`).  

Exemplo prático:  
```java
public class Exemplo {
    public static void main(String[] args) {
        int numero1 = 5;
        int numero2 = 3;
        int soma = numero1 + numero2;
        
        System.out.println("A soma é: " + soma); // Saída: "A soma é: 8"
    }
}
```

---

### **Resumo Final**  
✔ **Variável** = Espaço na memória que guarda um valor.  
✔ **Tipos primitivos** (`int`, `double`, etc.) → Armazenam valores diretamente.  
✔ **Variáveis de referência** (`String`, objetos) → Armazenam endereços de objetos.  
✔ **Métodos ≠ Variáveis** → Métodos são ações/funções.  

Se ainda tiver dúvidas, pode perguntar! 😊