Em Java, um **stream** é uma sequência de elementos que pode ser processada de forma sequencial ou paralela. Ele faz parte da API de **Streams**, introduzida no Java 8, e é projetado para facilitar o processamento de coleções (como listas, conjuntos e mapas) de forma funcional e declarativa.

---

### Características de um Stream
1. **Não armazena dados**:
   - Um stream não é uma estrutura de dados; ele apenas opera sobre uma fonte de dados (como uma lista ou array).

2. **Imutável**:
   - Um stream não modifica a coleção original. Em vez disso, ele cria um novo stream com os resultados das operações.

3. **Operações intermediárias e terminais**:
   - **Operações intermediárias**: Transformam o stream em outro stream (por exemplo, `filter`, `map`, `sorted`).
   - **Operações terminais**: Produzem um resultado ou efeito colateral (por exemplo, `forEach`, `collect`, `count`).

4. **Lazy evaluation (avaliação preguiçosa)**:
   - As operações intermediárias só são executadas quando uma operação terminal é chamada.

5. **Pode ser processado em paralelo**:
   - Streams podem ser facilmente convertidos em streams paralelos para processamento concorrente.

---

### Como criar um Stream?
Você pode criar um stream a partir de várias fontes de dados, como coleções, arrays, ou geradores.

#### Exemplos:
1. **A partir de uma lista**:
   ```java
   List<String> nomes = Arrays.asList("João", "Maria", "Ana");
   Stream<String> stream = nomes.stream();
   ```

2. **A partir de um array**:
   ```java
   String[] array = {"João", "Maria", "Ana"};
   Stream<String> stream = Arrays.stream(array);
   ```

3. **Usando `Stream.of`**:
   ```java
   Stream<String> stream = Stream.of("João", "Maria", "Ana");
   ```

4. **Streams de tipos primitivos**:
   ```java
   IntStream intStream = IntStream.range(1, 10); // Stream de inteiros de 1 a 9
   ```

---

### Operações comuns em Streams
Aqui estão algumas operações comuns que você pode realizar com streams:

#### 1. **Operações intermediárias**:
   - **`.filter(Predicate)`**: Filtra elementos com base em uma condição.
     ```java
     List<String> nomesComA = nomes.stream()
                                  .filter(nome -> nome.startsWith("A"))
                                  .collect(Collectors.toList());
     ```
   - **`.map(Function)`**: Transforma cada elemento usando uma função.
     ```java
     List<String> nomesMaiusculos = nomes.stream()
                                        .map(nome -> nome.toUpperCase())
                                        .collect(Collectors.toList());
     ```
   - **`.sorted()`**: Ordena os elementos.
     ```java
     List<String> nomesOrdenados = nomes.stream()
                                       .sorted()
                                       .collect(Collectors.toList());
     ```

#### 2. **Operações terminais**:
   - **`.forEach(Consumer)`**: Executa uma ação para cada elemento.
     ```java
     nomes.stream().forEach(nome -> System.out.println(nome));
     ```
   - **`.collect(Collector)`**: Coleta os elementos em uma coleção (lista, conjunto, etc.).
     ```java
     List<String> lista = nomes.stream().collect(Collectors.toList());
     ```
   - **`.count()`**: Retorna a quantidade de elementos no stream.
     ```java
     long quantidade = nomes.stream().count();
     ```
   - **`.reduce()`**: Combina os elementos do stream em um único resultado.
     ```java
     Optional<String> resultado = nomes.stream()
                                      .reduce((nome1, nome2) -> nome1 + ", " + nome2);
     ```

---

### Exemplo completo
Aqui está um exemplo completo que usa streams para processar uma lista de números:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class ExemploStream {
    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Filtra números pares, eleva ao quadrado e coleta em uma lista
        List<Integer> quadradosDosPares = numeros.stream()
                                               .filter(numero -> numero % 2 == 0) // Filtra pares
                                               .map(numero -> numero * numero)    // Eleva ao quadrado
                                               .collect(Collectors.toList());     // Coleta em uma lista

        System.out.println(quadradosDosPares); // [4, 16, 36, 64, 100]
    }
}
```

Neste exemplo:
1. `.filter(numero -> numero % 2 == 0)` filtra os números pares.
2. `.map(numero -> numero * numero)` eleva cada número par ao quadrado.
3. `.collect(Collectors.toList())` coleta os resultados em uma lista.

---

### Streams paralelos
Streams também podem ser processados em paralelo para melhorar o desempenho em operações intensivas. Basta usar o método `.parallelStream()` em vez de `.stream()`:

```java
List<Integer> quadradosDosPares = numeros.parallelStream()
                                        .filter(numero -> numero % 2 == 0)
                                        .map(numero -> numero * numero)
                                        .collect(Collectors.toList());
```

---

### Resumo
- Um **stream** é uma sequência de elementos que pode ser processada de forma funcional.
- Ele não armazena dados, mas opera sobre uma fonte de dados (como uma lista ou array).
- Oferece operações intermediárias (como `filter`, `map`, `sorted`) e terminais (como `forEach`, `collect`, `count`).
- Pode ser processado em paralelo para melhorar o desempenho.

Se precisar de mais exemplos ou explicações, é só perguntar! 😊
