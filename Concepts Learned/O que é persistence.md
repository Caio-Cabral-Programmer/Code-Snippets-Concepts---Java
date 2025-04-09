
Vou explicar o conceito de persistência de entidades de forma mais detalhada, especialmente para quem está começando com Java:

## Persistência de Entidades - Conceitos Básicos

### O que são entidades?

Entidades são classes Java que representam objetos do mundo real no seu sistema. No seu projeto, temos:

- `BoardEntity`: representa um quadro kanban
- `BoardColumnEntity`: representa uma coluna dentro do quadro (como "A fazer", "Em andamento")
- `CardEntity`: representa um cartão/tarefa que pode ser movido entre colunas
- `BlockEntity`: representa um bloqueio que pode ser aplicado a um cartão

Cada entidade corresponde geralmente a uma tabela no banco de dados.

### O que é persistência?

Persistência significa salvar dados de forma permanente, geralmente em um banco de dados. Quando você:

1. Cria um objeto Java (como um novo `BoardEntity`)
2. Preenche seus atributos (nome, descrição, etc.)
3. Chama um método para salvá-lo

O sistema converte esse objeto Java em registros no banco de dados para que os dados não sejam perdidos quando o programa for encerrado.

## Como funciona a persistência no seu projeto

### 1. Classes de Entidade (Entity)

Vamos analisar a classe `BoardEntity`:

```java
@Data
public class BoardEntity {
    private Long id;
    private String name;
    private List<BoardColumnEntity> boardColumns = new ArrayList<>();
    
    // Métodos auxiliares
}
```

- `@Data`: Esta anotação do Lombok gera automaticamente getters, setters, equals, hashCode e toString
- Os atributos (`id`, `name`) correspondem às colunas na tabela BOARDS do banco de dados
- A lista `boardColumns` representa um relacionamento "um para muitos" (um quadro tem várias colunas)

### 2. Classes DAO (Data Access Object)

O DAO é um padrão que encapsula a lógica de acesso ao banco de dados. Veja o `BoardDAO`:

```java
public class BoardDAO {
    private Connection connection;
    
    public BoardEntity insert(final BoardEntity entity) throws SQLException {
        var sql = "INSERT INTO BOARDS (name) values (?);";
        try(var statement = connection.prepareStatement(sql)){
            statement.setString(1, entity.getName());
            statement.executeUpdate();
            // Obtém o ID gerado e o atribui à entidade
            if (statement instanceof StatementImpl impl){
                entity.setId(impl.getLastInsertID());
            }
        }
        return entity;
    }
    
    // Outros métodos: delete, findById, findAll, etc.
}
```

Este código:
1. Recebe um objeto `BoardEntity` com dados
2. Cria uma instrução SQL para inserir esses dados no banco
3. Executa a instrução SQL
4. Atualiza o objeto com o ID gerado pelo banco
5. Retorna o objeto atualizado

### 3. Fluxo de persistência

Quando você quer salvar um novo quadro:

```java
// Em algum lugar do seu código
BoardEntity novoQuadro = new BoardEntity();
novoQuadro.setName("Meu Primeiro Quadro");

BoardDAO boardDAO = new BoardDAO(connection);
BoardEntity quadroSalvo = boardDAO.insert(novoQuadro);

System.out.println("Quadro salvo com ID: " + quadroSalvo.getId());
```

## Vantagens deste modelo

1. **Separação de responsabilidades**: O código que manipula os dados está separado do código que define a estrutura dos dados
2. **Reutilização**: Os métodos DAO podem ser usados em diferentes partes da aplicação
3. **Manutenção**: Se a estrutura do banco mudar, você só precisa atualizar o DAO, não toda a aplicação
4. **Testabilidade**: É mais fácil testar cada componente isoladamente

Para iniciantes em Java, entender este padrão é fundamental, pois é amplamente utilizado em aplicações empresariais e fornece uma base sólida para aprender frameworks mais avançados como Hibernate/JPA, que automatizam grande parte deste trabalho manual de persistência.
