Em Java, **nem todas as variáveis são objetos**, e **métodos não são variáveis**. Vamos esclarecer esses conceitos de forma simples, já que você está começando a aprender Java.  

### 1. **Variáveis em Java**  
Em Java, existem dois tipos principais de variáveis:  

#### **a) Variáveis primitivas**  
São tipos básicos que **não são objetos**. Elas armazenam valores diretamente. Exemplos:  

```java
int idade = 25;          // Tipo primitivo (não é um objeto)
double altura = 1.75;    // Tipo primitivo
char letra = 'A';        // Tipo primitivo
boolean ativo = true;    // Tipo primitivo
```

#### **b) Variáveis de referência (objetos)**  
São variáveis que **referenciam objetos** (instâncias de classes). Exemplos:  

```java
String nome = "João";       // String é um objeto
Scanner scanner = new Scanner(System.in); // Scanner é um objeto
```

### 2. **Métodos não são variáveis**  
Métodos são blocos de código que realizam uma ação. Eles podem:  
- Receber parâmetros (variáveis)  
- Retornar valores  
- Ser chamados em objetos ou classes  

Exemplo:  
```java
public class Exemplo {
    // Variável (atributo)
    int numero = 10;

    // Método (não é uma variável)
    public void imprimirNumero() {
        System.out.println(numero);
    }
}
```

### Resumo:  
✅ **Nem toda variável é um objeto** → Tipos primitivos (`int`, `double`, etc.) não são objetos.  
✅ **Variáveis de referência** (`String`, `Scanner`, etc.) apontam para objetos.  
❌ **Métodos não são variáveis** → Eles são ações/funções definidas em classes.  

Se tiver mais dúvidas, pode perguntar! 😊