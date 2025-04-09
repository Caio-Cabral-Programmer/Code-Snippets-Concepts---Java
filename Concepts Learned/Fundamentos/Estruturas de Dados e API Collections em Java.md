# Estruturas de Dados e a API Collections em Java (Para Iniciantes)

## O que são Estruturas de Dados?

Estruturas de dados são formas organizadas de armazenar e gerenciar dados em um programa. Elas definem como os dados são armazenados na memória e quais operações podem ser realizadas com esses dados.

Pense nelas como diferentes tipos de recipientes para organizar coisas:

- **Arrays**: Como uma caixa com compartimentos fixos
- **Listas**: Como uma fila de pessoas que pode crescer ou diminuir
- **Conjuntos**: Como uma bolsa onde cada item é único
- **Mapas**: Como um dicionário com pares palavra-significado

## A API Collections em Java

A API Collections é um conjunto de interfaces e classes no Java que implementam as principais estruturas de dados. Ela faz parte do pacote `java.util` e foi criada para facilitar o trabalho com grupos de objetos.

### Hierarquia Principal

1. **Collection** (interface raiz)
   - **List** (interface) - mantém ordem de inserção, permite duplicatas
   - **Set** (interface) - não permite duplicatas, não garante ordem
   - **Queue** (interface) - filas (FIFO) e pilhas (LIFO)

2. **Map** (interface separada) - armazena pares chave-valor

## Principais Implementações

### Listas (List)
- **ArrayList**: Lista baseada em array, acesso rápido por índice
```java
List<String> nomes = new ArrayList<>();
nomes.add("Ana");
nomes.add("Carlos");
nomes.get(0); // Retorna "Ana"
```

- **LinkedList**: Lista encadeada, melhor para inserções/remoções frequentes
```java
List<Integer> numeros = new LinkedList<>();
numeros.add(10);
numeros.add(20);
```

### Conjuntos (Set)
- **HashSet**: Conjunto sem ordem, usa hash table
```java
Set<String> emails = new HashSet<>();
emails.add("a@exemplo.com");
emails.add("b@exemplo.com");
```

- **TreeSet**: Conjunto ordenado
```java
Set<Integer> numeros = new TreeSet<>();
numeros.add(5);
numeros.add(1); // Ordena automaticamente
```

### Mapas (Map)
- **HashMap**: Mapa não ordenado chave-valor
```java
Map<String, Integer> idades = new HashMap<>();
idades.put("Ana", 25);
idades.put("Carlos", 30);
```

- **TreeMap**: Mapa ordenado por chave
```java
Map<String, Double> precos = new TreeMap<>();
precos.put("Notebook", 2500.0);
precos.put("Celular", 1500.0);
```

## Operações Comuns

Todas as collections compartilham operações básicas:

```java
// Adicionar elementos
collection.add(elemento);

// Remover elementos
collection.remove(elemento);

// Verificar tamanho
int tamanho = collection.size();

// Verificar se está vazio
boolean vazio = collection.isEmpty();

// Iterar sobre os elementos
for (Tipo elemento : collection) {
    System.out.println(elemento);
}
```

## Quando usar cada uma?

1. **ArrayList**: Quando precisa de acesso rápido por índice e não faz muitas inserções/remoções no meio
2. **LinkedList**: Quando faz muitas operações de inserção/remoção no início/meio
3. **HashSet**: Quando precisa verificar rapidamente se um elemento existe e a ordem não importa
4. **TreeSet**: Quando precisa de elementos únicos e ordenados
5. **HashMap**: Quando precisa associar chaves a valores de forma eficiente
6. **TreeMap**: Quando precisa de um mapa ordenado por chave

## Exemplo Prático Completo

```java
import java.util.*;

public class ExemploCollections {
    public static void main(String[] args) {
        // Lista de alunos
        List<String> alunos = new ArrayList<>();
        alunos.add("Maria");
        alunos.add("João");
        alunos.add("Ana");
        
        System.out.println("Lista de alunos: " + alunos);
        
        // Conjunto de números únicos
        Set<Integer> numeros = new HashSet<>();
        numeros.add(10);
        numeros.add(5);
        numeros.add(10); // Duplicado - não será adicionado
        
        System.out.println("Conjunto de números: " + numeros);
        
        // Mapa de notas por aluno
        Map<String, Double> notas = new HashMap<>();
        notas.put("Maria", 9.5);
        notas.put("João", 8.0);
        notas.put("Ana", 7.5);
        
        System.out.println("Notas de João: " + notas.get("João"));
        
        // Iterando sobre o mapa
        for (Map.Entry<String, Double> entry : notas.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

## Dicas para Iniciantes

1. Comece com ArrayList e HashMap - são as mais usadas
2. Use a interface (List, Set, Map) como tipo da variável, não a implementação
3. Explore os métodos utilitários da classe Collections (Collections.sort(), Collections.reverse(), etc.)
4. Pratique muito! Crie pequenos programas para testar cada estrutura

A API Collections é uma das partes mais úteis do Java. Dominá-la vai tornar seu código mais eficiente e legível.