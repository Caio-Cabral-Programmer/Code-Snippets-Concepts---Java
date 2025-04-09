# **Arrays em Java (Guia Completo para Iniciantes)**

Arrays são estruturas fundamentais em Java que permitem armazenar **múltiplos valores do mesmo tipo** em uma única variável. Vamos explorar tudo o que você precisa saber sobre arrays, desde a declaração até operações avançadas.

## **1. O que é um Array?**
Um array é uma **estrutura de tamanho fixo** que armazena elementos do mesmo tipo:
- Todos os elementos são do mesmo tipo (ex: todos `int`, todos `String`)
- Tamanho definido na criação e não pode ser alterado depois
- Acesso aos elementos por **índices** (posições), começando em 0

---

## **2. Declarando e Inicializando Arrays**

### **Forma 1: Declaração + Inicialização Explícita**
```java
tipo[] nomeDoArray = {valor1, valor2, ..., valorN};
```
Exemplo:
```java
int[] numeros = {10, 20, 30, 40, 50};
String[] frutas = {"Maçã", "Banana", "Laranja"};
```

### **Forma 2: Declaração + Tamanho (Valores Padrão)**
```java
tipo[] nomeDoArray = new tipo[tamanho];
```
Exemplo:
```java
double[] precos = new double[4]; // [0.0, 0.0, 0.0, 0.0]
boolean[] flags = new boolean[3]; // [false, false, false]
```

### **Forma 3: Declaração Separada da Inicialização**
```java
int[] numeros;
numeros = new int[]{5, 10, 15};
```

---

## **3. Acessando Elementos do Array**
Os elementos são acessados pelo **índice** (posição), começando em 0:
```java
int[] numeros = {10, 20, 30};
System.out.println(numeros[0]); // 10 (primeiro elemento)
System.out.println(numeros[1]); // 20
System.out.println(numeros[2]); // 30 (último elemento)
```

### **Exceção Comum: `ArrayIndexOutOfBoundsException`**
Acontece ao tentar acessar um índice inválido:
```java
System.out.println(numeros[3]); // ERRO! Índice máximo é 2
```

---

## **4. Tamanho do Array (`length`)**
Use `.length` para obter o tamanho (não é um método, é um atributo):
```java
String[] carros = {"Fusca", "Gol", "Uno"};
System.out.println(carros.length); // 3
```

---

## **5. Percorrendo Arrays (Iteração)**

### **Método 1: Loop `for` Tradicional**
```java
int[] notas = {8, 9, 7, 6};
for (int i = 0; i < notas.length; i++) {
    System.out.println("Nota " + i + ": " + notas[i]);
}
```

### **Método 2: Enhanced `for` (for-each)**
Mais simples quando não precisa do índice:
```java
for (int nota : notas) {
    System.out.println("Nota: " + nota);
}
```

---

## **6. Arrays Multidimensionais (Matrizes)**
Arrays de arrays (útil para tabelas, grids):

### **Declaração de Matriz 2D**
```java
int[][] matriz = new int[3][3]; // 3 linhas x 3 colunas
```

### **Inicialização Direta**
```java
int[][] tabuleiro = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

### **Acesso a Elementos**
```java
System.out.println(tabuleiro[1][2]); // 6 (linha 1, coluna 2)
```

### **Percorrendo Matrizes**
```java
for (int i = 0; i < tabuleiro.length; i++) {
    for (int j = 0; j < tabuleiro[i].length; j++) {
        System.out.print(tabuleiro[i][j] + " ");
    }
    System.out.println();
}
```

---

## **7. Operações Comuns com Arrays**

### **Preenchendo um Array**
```java
int[] valores = new int[5];
Arrays.fill(valores, 100); // [100, 100, 100, 100, 100]
```

### **Ordenação (`Arrays.sort()`)**
```java
int[] numeros = {5, 3, 9, 1};
Arrays.sort(numeros); // [1, 3, 5, 9]
```

### **Busca Binária (`Arrays.binarySearch()`)**
```java
int posicao = Arrays.binarySearch(numeros, 5); // 2 (índice do valor 5)
```

### **Copiando Arrays**
```java
int[] copia = Arrays.copyOf(numeros, numeros.length);
```

---

## **8. Limitações dos Arrays**
- **Tamanho fixo**: Não pode crescer/diminuir dinamicamente.
- **Métodos limitados**: Para operações complexas, use `ArrayList` ou outras coleções.

---

## **9. Exemplo Completo**
```java
public class ExemploArray {
    public static void main(String[] args) {
        // Declaração e inicialização
        String[] cidades = {"São Paulo", "Rio", "Belo Horizonte"};
        
        // Acessando elementos
        System.out.println(cidades[0]); // São Paulo
        
        // Alterando valor
        cidades[1] = "Salvador";
        
        // Iteração com for-each
        for (String cidade : cidades) {
            System.out.println(cidade);
        }
        
        // Matriz 2D
        int[][] matriz = {{1, 2}, {3, 4}};
        System.out.println(matriz[1][0]); // 3
    }
}
```

---

## **10. Quando Usar Arrays?**
✔ Quando você sabe o número exato de elementos antecipadamente  
✔ Para armazenar tipos primitivos ou objetos de forma eficiente  
✔ Em operações de baixo nível que requerem performance  

Para casos mais flexíveis, considere **`ArrayList`** (que cresce dinamicamente).

---

### **Resumo Final**
- **Arrays armazenam múltiplos valores do mesmo tipo**  
- **Índices começam em 0**  
- **Tamanho fixo** (use `length` para obter o tamanho)  
- **Pode ser unidimensional ou multidimensional**  
- **Use `Arrays.sort()`, `Arrays.copyOf()` para operações úteis**  

Pratique criando e manipulando arrays para fixar o conceito! 😊