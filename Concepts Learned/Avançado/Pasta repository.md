# **A Pasta Repository no Spring Boot - Guia Completo para Iniciantes**

Olá, futuro desenvolvedor Spring! 👋 Vamos explorar juntos o mundo dos repositórios no Spring Boot como se estivéssemos construindo uma biblioteca mágica de dados!

## **1. O Que é a Pasta Repository? (Sua Caixa de Tesouros de Dados)**

Imagine que você tem:

- 📚 **Livros** (seus dados)
- 🏰 **Uma biblioteca** (seu banco de dados)
- 🧙 **Um bibliotecário mágico** (o repositório)

A pasta `repository` é onde moram esses "bibliotecários mágicos" que sabem exatamente onde cada informação está guardada!

## **2. Modo Antigo vs Modo Moderno**

### **🔹 Sem Spring Data JPA (Modo Trabalhoso)**
```java
// PessoaDAO.java - Modo antigo (JDBC puro)
public class PessoaDAO {
    public Pessoa findById(int id) {
        Connection conn = null;
        PreparedStatement stmt = null;
        try {
            conn = DriverManager.getConnection("jdbc:mysql...");
            stmt = conn.prepareStatement("SELECT * FROM pessoas WHERE id = ?");
            stmt.setInt(1, id);
            ResultSet rs = stmt.executeQuery();
            
            if (rs.next()) {
                Pessoa p = new Pessoa();
                p.setId(rs.getInt("id"));
                p.setNome(rs.getString("nome"));
                return p;
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // Fechar conexões manualmente!
        }
        return null;
    }
    // +20 métodos similares para cada operação...
}
```
**Problemas:**
- Muito código repetitivo
- Fácil cometer erros
- Difícil de manter

### **🔹 Com Spring Data JPA (Modo Mágico)**
```java
// PessoaRepository.java - Modo moderno
@Repository
public interface PessoaRepository extends JpaRepository<Pessoa, Long> {
    // Método mágico que o Spring implementa sozinho!
    List<Pessoa> findByNomeContaining(String nome);
}
```

**Mágica do Spring:**
```java
// Uso no serviço
@Service
public class PessoaService {
    @Autowired
    private PessoaRepository repo;  // O Spring injeta automaticamente
    
    public List<Pessoa> buscarPorNome(String nome) {
        return repo.findByNomeContaining(nome);  // Funciona como mágica!
    }
}
```

## **3. Por Que Usar JpaRepository? (Seu Superpoder)**

Quando você faz:
```java
public interface PessoaRepository extends JpaRepository<Pessoa, Long>
```

Você está ganhando **superpoderes** gratuitamente:

| Método Mágico          | O Que Faz?                  | SQL Equivalente (que você NÃO precisa escrever) |
|------------------------|----------------------------|------------------------------------------------|
| `save(entity)`         | Salva ou atualiza          | INSERT/UPDATE                                  |
| `findById(id)`         | Busca por ID               | SELECT * FROM tabela WHERE id = ?              |
| `findAll()`            | Lista todos                | SELECT * FROM tabela                           |
| `deleteById(id)`       | Remove por ID              | DELETE FROM tabela WHERE id = ?                |
| `count()`              | Conta registros            | SELECT COUNT(*) FROM tabela                    |

## **4. Quando Criar um Repositório?**

Crie um repositório sempre que:
1. Você tem uma **entidade** (classe com `@Entity`)
2. Precisa **guardar/ler** dados no banco
3. Quer **evitar escrever SQL** manualmente

Exemplo completo:

```java
// 1. Entidade
@Entity
public class Livro {
    @Id
    @GeneratedValue
    private Long id;
    private String titulo;
    private String autor;
    // getters/setters
}

// 2. Repositório
@Repository
public interface LivroRepository extends JpaRepository<Livro, Long> {
    // Consulta personalizada
    List<Livro> findByAutorOrderByTitulo(String autor);
}

// 3. Uso no serviço
@Service
public class BibliotecaService {
    @Autowired
    private LivroRepository livroRepo;
    
    public List<Livro> livrosDoAutor(String autor) {
        return livroRepo.findByAutorOrderByTitulo(autor);
    }
}
```

## **5. Consultas Personalizadas (Sua Varinha Mágica)**

Você pode criar consultas especiais de três formas:

### **1. Métodos de Nome Mágico**
```java
List<Livro> findByTituloContainingIgnoreCase(String termo);
// SELECT * FROM livro WHERE UPPER(titulo) LIKE UPPER(%termo%)
```

### **2. @Query (Para feitiços complexos)**
```java
@Query("SELECT l FROM Livro l WHERE l.autor = :autor AND l.anoPublicacao > :ano")
List<Livro> livrosRecentesDoAutor(@Param("autor") String autor, @Param("ano") int ano);
```

### **3. Query Nativa (Quando precisa de SQL puro)**
```java
@Query(value = "SELECT * FROM livros WHERE titulo LIKE %:termo%", nativeQuery = true)
List<Livro> buscaPorTermoNativo(@Param("termo") String termo);
```

## **6. Boas Práticas (O Livro de Regras Mágicas)**

✅ **Organize por domínio**: 
   - `com.empresa.produto.repositories` (para produtos)
   - `com.empresa.vendas.repositories` (para vendas)

✅ **Use nomes claros**:
   - `ClienteRepository` (bom)
   - `RepoCli` (ruim)

✅ **Evite lógica de negócio** no repositório:
   - O repositório só acessa dados
   - Regras de negócio ficam nos Services

✅ **Prefira métodos derivados** a @Query quando possível:
   - `findByNomeContaining` (melhor)
   - `@Query("SELECT x FROM...")` (só quando necessário)

## **7. Dicas Mágicas Avançadas**

### **Paginação (Para listas grandes)**
```java
Page<Livro> findAll(Pageable pageable);

// Uso:
Page<Livro> pagina = livroRepo.findAll(PageRequest.of(0, 10));
// Página 0, 10 registros por página
```

### **Auditoria (Quem e quando alterou)**
```java
@Entity
@EntityListeners(AuditingEntityListener.class)
public class Livro {
    // ...
    @CreatedDate
    private LocalDateTime dataCriacao;
    
    @LastModifiedBy
    private String ultimoEditor;
}
```

## **8. Quando NÃO Usar?**

❌ Em projetos muito simples (talvez um `CrudRepository` baste)  
❌ Quando precisa de controle total sobre o SQL  
❌ Em sistemas legados que não usam Spring  

## **Resumo da Magia**

| **Sem JpaRepository**          | **Com JpaRepository**          |
|--------------------------------|--------------------------------|
| Escreve SQL manualmente        | Gera SQL automaticamente       |
| Classes DAO cheias de código   | Interfaces limpas              |
| Risco de erros SQL             | Quase zero erros de sintaxe    |
| Atualizações demoradas         | Fácil manutenção               |

**Exemplo Final Completo:**
```java
// Entidade
@Entity
@Data // Lombok para getters/setters
public class Aluno {
    @Id
    @GeneratedValue
    private Long matricula;
    private String nome;
    private String curso;
}

// Repositório
@Repository
public interface AlunoRepository extends JpaRepository<Aluno, Long> {
    List<Aluno> findByCurso(String curso);
    List<Aluno> findByNomeStartingWith(String prefixo);
}

// Serviço
@Service
@RequiredArgsConstructor // Lombok para injetar dependência
public class EscolaService {
    private final AlunoRepository alunoRepo;
    
    public List<Aluno> alunosDoCurso(String curso) {
        return alunoRepo.findByCurso(curso);
    }
}
```

Agora você já pode começar a criar seus próprios repositórios mágicos! ✨ Qual parte você gostaria de explorar mais?