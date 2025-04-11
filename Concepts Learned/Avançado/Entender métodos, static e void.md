# **Métodos, `static` e `void` em Java (Explicação Detalhada para Iniciantes)**

Em Java, **métodos** são blocos de código que realizam tarefas específicas. Eles podem receber dados (parâmetros), processá-los e retornar um resultado (ou não).  
As palavras-chave **`static`** e **`void`** modificam o comportamento dos métodos. Vamos entender cada um em detalhes.

---

## **1. O que são Métodos em Java?**  
Um **método** é uma função dentro de uma classe que executa uma ação. Ele pode:
- **Receber parâmetros** (dados de entrada)
- **Processar esses dados**
- **Retornar um resultado** (ou não, se for `void`)

### **Estrutura Básica de um Método:**
```java
[modificador] [tipo de retorno] [nome do método]([parâmetros]) {
    // Corpo do método (código que executa a tarefa)
    return [valor]; // (Opcional, se não for void)
}
```

### **Exemplo de Método:**
```java
public int somar(int a, int b) {
    int resultado = a + b;
    return resultado;
}
```
- **`public`** → Modificador de acesso (pode ser chamado de qualquer lugar)
- **`int`** → Tipo de retorno (retorna um número inteiro)
- **`somar`** → Nome do método
- **`(int a, int b)`** → Parâmetros (dados de entrada)
- **`return resultado;`** → Retorna o valor calculado

---

## **2. O que é `void` em Java?**  
O **`void`** indica que um método **não retorna nenhum valor**. Ele apenas executa uma ação.

### **Exemplo de Método `void`:**
```java
public void imprimirMensagem(String mensagem) {
    System.out.println(mensagem);
    // Não tem 'return', pois é void
}
```
- **`void`** → Significa "sem retorno"
- **`imprimirMensagem`** → Apenas imprime a mensagem, mas não devolve nada.

### **Quando usar `void`?**
- Quando o método só executa uma ação (ex: imprimir, salvar no banco de dados, alterar um valor).
- Quando não é necessário retornar um resultado.

---

## **3. O que é `static` em Java?**  
O **`static`** define que um método (ou variável) **pertence à classe**, e não a um objeto específico. Isso significa que você pode chamá-lo **sem criar uma instância da classe**.

### **Exemplo de Método `static`:**
```java
public class Calculadora {
    public static int somar(int a, int b) {
        return a + b;
    }
}
```
- **`static`** → Permite chamar o método diretamente pela classe, sem instanciar um objeto.

### **Como chamar um método `static`?**
```java
int resultado = Calculadora.somar(5, 3); // Não precisa de 'new Calculadora()'
System.out.println(resultado); // Saída: 8
```

### **Quando usar `static`?**
- Para métodos utilitários (ex: cálculos matemáticos, formatação de texto).
- Quando o método não depende do estado de um objeto (não usa variáveis de instância).

---

## **Diferença entre Métodos `static` e Não-`static`**
| **Característica**       | **Método `static`**                          | **Método Não-`static` (de instância)**          |
|--------------------------|---------------------------------------------|-----------------------------------------------|
| **Pertence a**           | Classe                                      | Objeto (instância da classe)                  |
| **Pode ser chamado sem instância?** | Sim (`Classe.metodo()`) | Não (precisa de `new Classe().metodo()`) |
| **Acessa variáveis de instância?** | ❌ Não (só variáveis `static`) | ✅ Sim |
| **Exemplo**              | `Math.sqrt(16)`                             | `lista.add("Item")`                           |

---

## **Resumo Final**
1. **Métodos** → Blocos de código que executam tarefas.
2. **`void`** → Indica que o método não retorna valor.
3. **`static`** → Permite chamar o método sem criar um objeto.

### **Exemplo Combinando `static` e `void`:**
```java
public class Exemplo {
    public static void main(String[] args) { // Método static e void
        imprimirOi(); // Chamada direta (static)
    }

    public static void imprimirOi() { // static + void
        System.out.println("Oi!");
    }
}
```

### **Quando Usar Cada Um?**
| **Caso de Uso**               | **Tipo de Método**          |
|-------------------------------|----------------------------|
| Método utilitário (não depende de objetos) | `static` |
| Método que não retorna valor | `void` |
| Método que opera em dados de um objeto | Não-`static` |
| Método que retorna um valor | Definir tipo de retorno (`int`, `String`, etc.) |

Espero que esta explicação tenha esclarecido os conceitos! Se ainda tiver dúvidas, pode perguntar. 😊