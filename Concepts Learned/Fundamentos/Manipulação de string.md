# **Manipulação de Strings em Java (Guia para Iniciantes)**  

Em Java, **String** é uma sequência de caracteres (letras, números, símbolos) e é uma das classes mais usadas. Vamos explorar **como criar, comparar, modificar e extrair informações** de Strings.  

---

## **1. Criando Strings**  

Há duas formas principais de criar uma String:  

### **a) Usando Literais de String (Recomendado para maioria dos casos)**  
```java
String nome = "Java"; // Armazenada no "String Pool" (mais eficiente)
```  

### **b) Usando o Construtor `new` (Cria um novo objeto na memória)**  
```java
String nome = new String("Java"); // Objeto separado (evitar se não necessário)
```  

🔹 **Diferença:**  
- Literais (`"Java"`) são reutilizados se já existirem no *String Pool*.  
- `new String()` sempre cria um novo objeto, mesmo que o conteúdo seja igual.  

---

## **2. Operações Básicas com Strings**  

### **a) Concatenar (Juntar Strings)**  
```java
String saudacao = "Olá, " + "Mundo!"; // "Olá, Mundo!"
```  
Ou com `concat()`:  
```java
String nome = "Ana".concat(" Maria"); // "Ana Maria"
```  

### **b) Tamanho da String (`length()`)**  
```java
String texto = "Java";
int tamanho = texto.length(); // 4
```  

### **c) Acessar Caracteres (`charAt()`)**  
```java
char primeiraLetra = "Java".charAt(0); // 'J' (índice começa em 0)
```  

### **d) Converter para Maiúsculas/Minúsculas**  
```java
String maiuscula = "java".toUpperCase(); // "JAVA"
String minuscula = "JAVA".toLowerCase(); // "java"
```  

### **e) Remover Espaços em Branco (`trim()`)**  
```java
String comEspacos = "  Java  ";
String semEspacos = comEspacos.trim(); // "Java"
```  

---

## **3. Comparação de Strings**  

### **a) `equals()` (Comparação de Conteúdo)**  
```java
String s1 = "Java";
String s2 = new String("Java");

System.out.println(s1.equals(s2)); // true (conteúdo igual)
```  

### **b) `==` (Comparação de Referência - Evitar para Strings!)**  
```java
System.out.println(s1 == s2); // false (objetos diferentes na memória)
```  

🔹 **Regra:** Sempre use `equals()` para comparar Strings!  

### **c) `equalsIgnoreCase()` (Ignora Maiúsculas/Minúsculas)**  
```java
System.out.println("java".equalsIgnoreCase("JAVA")); // true
```  

---

## **4. Busca e Extração de Strings**  

### **a) Verificar se contém uma substring (`contains()`)**  
```java
String frase = "Java é divertido";
boolean contem = frase.contains("divertido"); // true
```  

### **b) Encontrar posição de uma substring (`indexOf()`)**  
```java
int posicao = frase.indexOf("é"); // 5 (retorna -1 se não encontrar)
```  

### **c) Extrair parte da String (`substring()`)**  
```java
String palavra = frase.substring(0, 4); // "Java" (índices 0 a 3)
```  

---

## **5. Substituição e Divisão**  

### **a) Substituir caracteres (`replace()`)**  
```java
String novaFrase = frase.replace("divertido", "poderoso"); // "Java é poderoso"
```  

### **b) Dividir String em partes (`split()`)**  
```java
String[] palavras = frase.split(" "); // ["Java", "é", "divertido"]
```  

---

## **6. Formatação de Strings**  

### **a) `String.format()` (Similar ao printf)**  
```java
String mensagem = String.format("Olá, %s! Você tem %d anos.", "Ana", 25);
// Saída: "Olá, Ana! Você tem 25 anos."
```  

### **b) `String.join()` (Juntar Strings com delimitador)**  
```java
String resultado = String.join("-", "Java", "Python", "C++"); // "Java-Python-C++"
```  

---

## **7. Strings são Imutáveis!**  

- **Toda String em Java é imutável** (não pode ser alterada depois de criada).  
- Métodos como `replace()`, `toUpperCase()`, etc., **retornam uma nova String**.  

Exemplo:  
```java
String original = "java";
original.toUpperCase(); // Não altera "original"!
System.out.println(original); // "java" (continua minúscula)

String modificada = original.toUpperCase(); // Agora sim, nova String
System.out.println(modificada); // "JAVA"
```  

---

## **8. StringBuilder (Para Muitas Modificações)**  

Se você precisa fazer **muitas alterações em uma String**, use `StringBuilder` (mais eficiente):  

```java
StringBuilder sb = new StringBuilder("Java");
sb.append(" é ").append("legal!"); // "Java é legal!"
String resultado = sb.toString();
```  

🔹 **Vantagens:**  
- Evita criar múltiplos objetos String.  
- Melhor desempenho em loops e concatenações complexas.  

---

## **Exemplo Completo**  

```java
public class ExemploStrings {
    public static void main(String[] args) {
        String nome = "Java";
        
        // Concatenar
        String saudacao = "Olá, " + nome + "!"; // "Olá, Java!"
        
        // Tamanho
        int tamanho = nome.length(); // 4
        
        // Maiúsculas
        String gritando = nome.toUpperCase(); // "JAVA"
        
        // Substituir
        String novaString = nome.replace('a', '4'); // "J4v4"
        
        // Dividir
        String linguagens = "Java-Python-C++";
        String[] array = linguagens.split("-"); // ["Java", "Python", "C++"]
        
        System.out.println(saudacao);
        System.out.println("Tamanho: " + tamanho);
        System.out.println("Maiúsculas: " + gritando);
        System.out.println("Substituído: " + novaString);
        System.out.println("Primeira linguagem: " + array[0]);
    }
}
```

---

## **Resumo das Principais Operações**  

| Operação                | Método                   | Exemplo                          |
|-------------------------|--------------------------|----------------------------------|
| **Concatenar**          | `+` ou `concat()`        | `"A" + "B"` → `"AB"`             |
| **Tamanho**             | `length()`               | `"Java".length()` → `4`          |
| **Acessar caractere**   | `charAt()`               | `"Java".charAt(0)` → `'J'`       |
| **Maiúsculas**          | `toUpperCase()`          | `"java".toUpperCase()` → `"JAVA"`|
| **Minúsculas**          | `toLowerCase()`          | `"JAVA".toLowerCase()` → `"java"`|
| **Remover espaços**     | `trim()`                 | `"  a  ".trim()` → `"a"`         |
| **Comparar**            | `equals()`               | `"A".equals("A")` → `true`       |
| **Substring**           | `substring()`            | `"Java".substring(1)` → `"ava"`  |
| **Substituir**          | `replace()`              | `"a".replace('a', 'b')` → `"b"`  |
| **Dividir**             | `split()`                | `"A-B".split("-")` → `["A", "B"]`|

---

### **Conclusão**  
- **Strings são imutáveis**: Qualquer modificação gera uma nova String.  
- **Use `equals()` para comparar conteúdo**, nunca `==`.  
- **Para muitas concatenações**, prefira `StringBuilder`.  

Se tiver dúvidas sobre algum método específico, pode perguntar! 😊