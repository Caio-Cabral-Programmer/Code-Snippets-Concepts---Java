O **Lombok** é uma biblioteca Java que ajuda a reduzir a quantidade de código repetitivo e boilerplate (código padrão que é escrito várias vezes) em suas classes. Ele faz isso através de anotações que geram código automaticamente em tempo de compilação. Isso torna o código mais limpo, legível e fácil de manter.

---

### Principais funcionalidades do Lombok
O Lombok oferece várias anotações úteis para simplificar o desenvolvimento. Aqui estão algumas das mais comuns:

1. **`@Getter` e `@Setter`**:
   - Gera automaticamente métodos `get` e `set` para os campos da classe.
   - Exemplo:
     ```java
     import lombok.Getter;
     import lombok.Setter;

     @Getter
     @Setter
     public class Pessoa {
         private String nome;
         private int idade;
     }
     ```
     Isso equivale a escrever manualmente os métodos `getNome()`, `setNome()`, `getIdade()` e `setIdade()`.

2. **`@ToString`**:
   - Gera automaticamente o método `toString()` para a classe.
   - Exemplo:
     ```java
     import lombok.ToString;

     @ToString
     public class Pessoa {
         private String nome;
         private int idade;
     }
     ```
     Isso gera um `toString()` que retorna algo como `"Pessoa(nome=João, idade=30)"`.

3. **`@EqualsAndHashCode`**:
   - Gera automaticamente os métodos `equals()` e `hashCode()` com base nos campos da classe.
   - Exemplo:
     ```java
     import lombok.EqualsAndHashCode;

     @EqualsAndHashCode
     public class Pessoa {
         private String nome;
         private int idade;
     }
     ```

4. **`@NoArgsConstructor`, `@RequiredArgsConstructor` e `@AllArgsConstructor`**:
   - Geram construtores automaticamente.
     - `@NoArgsConstructor`: Cria um construtor sem argumentos.
     - `@RequiredArgsConstructor`: Cria um construtor com argumentos para campos `final` ou `@NonNull`.
     - `@AllArgsConstructor`: Cria um construtor com todos os argumentos.
   - Exemplo:
     ```java
     import lombok.AllArgsConstructor;
     import lombok.NoArgsConstructor;
     import lombok.RequiredArgsConstructor;

     @NoArgsConstructor
     @RequiredArgsConstructor
     @AllArgsConstructor
     public class Pessoa {
         private String nome;
         private int idade;
     }
     ```

5. **`@Data`**:
   - Combina várias anotações: `@Getter`, `@Setter`, `@ToString`, `@EqualsAndHashCode` e `@RequiredArgsConstructor`.
   - Exemplo:
     ```java
     import lombok.Data;

     @Data
     public class Pessoa {
         private String nome;
         private int idade;
     }
     ```

6. **`@Builder`**:
   - Implementa o padrão de projeto **Builder** para a classe, permitindo a criação de objetos de forma fluente.
   - Exemplo:
     ```java
     import lombok.Builder;

     @Builder
     public class Pessoa {
         private String nome;
         private int idade;
     }

     // Uso
     Pessoa pessoa = Pessoa.builder()
                           .nome("João")
                           .idade(30)
                           .build();
     ```

7. **`@Slf4j`**:
   - Adiciona automaticamente um logger (usando a biblioteca SLF4J) à classe.
   - Exemplo:
     ```java
     import lombok.extern.slf4j.Slf4j;

     @Slf4j
     public class MinhaClasse {
         public void fazerAlgo() {
             log.info("Fazendo algo...");
         }
     }
     ```

---

### Como usar o Lombok no seu projeto
1. **Adicionar a dependência**:
   - No Maven, adicione ao `pom.xml`:
     ```xml
     <dependency>
         <groupId>org.projectlombok</groupId>
         <artifactId>lombok</artifactId>
         <version>1.18.24</version> <!-- Verifique a versão mais recente -->
         <scope>provided</scope>
     </dependency>
     ```
   - No Gradle, adicione ao `build.gradle`:
     ```groovy
     dependencies {
         compileOnly 'org.projectlombok:lombok:1.18.24'
         annotationProcessor 'org.projectlombok:lombok:1.18.24'
     }
     ```

2. **Instalar o plugin do Lombok na IDE**:
   - Para que sua IDE reconheça as anotações do Lombok e não mostre erros, você precisa instalar o plugin do Lombok. Isso é especialmente importante para IDEs como IntelliJ IDEA e Eclipse.

3. **Habilitar o processamento de anotações**:
   - Certifique-se de que o processamento de anotações (annotation processing) está habilitado na sua IDE.

---

### Vantagens do Lombok
- **Redução de código boilerplate**: Menos código para escrever e manter.
- **Código mais limpo**: Foca no que é importante, sem distrações com métodos repetitivos.
- **Produtividade**: Economiza tempo ao gerar automaticamente métodos comuns.

---

### Desvantagens do Lombok
- **Dependência externa**: Adiciona uma dependência ao projeto.
- **Curva de aprendizado**: Pode ser confuso para quem não está familiarizado com as anotações.
- **Compatibilidade**: Pode haver problemas de compatibilidade com algumas ferramentas ou versões de IDEs.

---

### Resumo
O Lombok é uma biblioteca poderosa que simplifica o desenvolvimento Java, eliminando código repetitivo e melhorando a legibilidade. Ele é amplamente utilizado em projetos modernos, mas é importante entender suas funcionalidades e configurá-lo corretamente.

Se precisar de mais exemplos ou ajuda para configurar o Lombok no seu projeto, é só perguntar! 😊
