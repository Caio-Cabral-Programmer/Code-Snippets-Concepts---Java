Vamos explicar detalhadamente o código `var statement = connection.prepareStatement(sql)` em Java, que é fundamental para trabalhar com bancos de dados usando JDBC (Java Database Connectivity).

### O que essa linha faz?
Esta linha cria um objeto `PreparedStatement` a partir de uma conexão (`Connection`) com um banco de dados, preparando uma consulta SQL para execução.

### Desmembrando cada parte:

1. **`var` (Java 10+)**
   - Palavra-chave que permite inferência de tipos local
   - O compilador deduz que `statement` será do tipo `PreparedStatement`
   - Equivalente a: `PreparedStatement statement = connection.prepareStatement(sql)`

2. **`connection`**
   - Objeto do tipo `java.sql.Connection`
   - Representa uma conexão ativa com o banco de dados
   - Foi obtido anteriormente através de `DriverManager.getConnection()`

3. **`.prepareStatement()`**
   - Método da interface `Connection`
   - Cria um objeto `PreparedStatement` para enviar comandos SQL parametrizados
   - Vantagens sobre `createStatement()`:
     * Previne SQL injection
     * Melhor desempenho para execuções repetidas
     * Tratamento adequado de tipos de dados

4. **`sql`**
   - String contendo o comando SQL a ser executado
   - Pode conter parâmetros representados por `?`
   - Exemplo: `"SELECT * FROM users WHERE id = ?"`

### Como funciona internamente:
1. O driver JDBC analisa e pré-compila a query SQL
2. Cria um objeto `PreparedStatement` com a query preparada
3. Retorna uma referência para esse objeto

### Exemplo completo de uso:
```java
// 1. Estabelecer conexão
try (Connection connection = DriverManager.getConnection(url, user, password)) {
    
    // 2. Preparar statement
    String sql = "INSERT INTO products (name, price) VALUES (?, ?)";
    var statement = connection.prepareStatement(sql);
    
    // 3. Definir parâmetros
    statement.setString(1, "Notebook");
    statement.setDouble(2, 2999.90);
    
    // 4. Executar
    int rowsAffected = statement.executeUpdate();
    
} catch (SQLException e) {
    e.printStackTrace();
}
```

### Por que usar PreparedStatement?
1. **Segurança**: Protege contra SQL injection
2. **Performance**: O mesmo statement pode ser reutilizado com diferentes parâmetros
3. **Legibilidade**: Separa claramente o SQL dos valores
4. **Tratamento de tipos**: Conversão automática entre tipos Java e SQL

### Observações importantes:
- O `PreparedStatement` deve ser fechado após o uso (idealmente com try-with-resources)
- Os parâmetros (?) são indexados a partir de 1, não de 0
- Existem variações como `prepareStatement(sql, RETURN_GENERATED_KEYS)` para obter IDs auto-incrementados

Esta abordagem é a forma recomendada de executar queries SQL parametrizadas em Java, sendo mais segura e eficiente que concatenar strings SQL manualmente.
