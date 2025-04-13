# 🧩 Regras de Negócio: O "Cérebro" dos Sistemas Java

Vamos imaginar que você está abrindo uma lojinha de doces! 🍭 Tudo o que você precisa decidir sobre como a loja funciona são suas **regras de negócio**.

## 🌟 O que são Regras de Negócio?

São as **leis do seu sistema** - como um manual de instruções que diz:

1. **O que pode** ou **não pode** acontecer
2. **Como** as coisas devem acontecer
3. **Quando** algo deve acontecer

### Exemplo na Loja de Doces:
- "Só vendo balas para maiores de 3 anos" (regra)
- "Desconto de 10% para compras acima de R$ 20" (regra)
- "Todo pagamento em dinheiro precisa de troco" (regra)

## 🏗️ Onde elas ficam no código?

### Modo Antigo (Bagunçado):
```java
public class VendaServlet extends HttpServlet {
    protected void doPost(...) {
        // Tudo misturado!
        // 1. Verifica idade (regra)
        // 2. Calcula desconto (regra)
        // 3. Salva no banco (tecnologia)
        // 4. Manda email (tecnologia)
    }
}
```
**Problema**: Se a regra mudar, é difícil achar onde alterar!

### Modo Moderno (Organizado):
```java
@Service
public class VendaService {
    
    // Regra 1: Verificar idade
    public boolean podeComprar(int idade) {
        return idade > 3;
    }
    
    // Regra 2: Calcular desconto
    public BigDecimal calcularDesconto(BigDecimal valor) {
        return valor.compareTo(new BigDecimal("20")) > 0 
               ? valor.multiply(new BigDecimal("0.1")) 
               : BigDecimal.ZERO;
    }
}
```

## 📜 Tipos de Regras de Negócio

1. **Regras de Validação** (O que **NÃO** pode)
   ```java
   if (cliente.getIdade() < 18 && produto.isAdulto()) {
       throw new RegraNegocioException("Menores não podem comprar este produto");
   }
   ```

2. **Regras de Cálculo** (Como calcular coisas)
   ```java
   public BigDecimal calcularImposto(Produto p) {
       return p.getPreco()
               .multiply(p.getCategoria().getAliquota());
   }
   ```

3. **Regras de Fluxo** (Quando fazer algo)
   ```java
   if (pedido.getValor() > 1000) {
       notificarGerente(pedido);
   }
   ```

## ⚔️ Modo Arcaico vs. Moderno

### Sem Tecnologia (Anos 90):
```java
public class Main {
    public static void main(String[] args) {
        // Tudo junto e misturado
        if (idade < 18) { // Regra solta no código
            System.out.println("Não pode comprar!");
        }
    }
}
```

### Com Tecnologia (Spring Boot 2023):
```java
@Service
public class ValidadorService {
    private final IdadeValidator idadeValidator;
    private final CpfValidator cpfValidator;

    @Autowired
    public ValidadorService(IdadeValidator iv, CpfValidator cv) {
        this.idadeValidator = iv;
        this.cpfValidator = cv;
    }

    public void validar(Cliente cliente) {
        idadeValidator.validar(cliente.getIdade());
        cpfValidator.validar(cliente.getCpf());
    }
}

// Classe dedicada só para validar idade
@Component
public class IdadeValidator {
    public void validar(int idade) {
        if (idade < 18) throw new RegraNegocioException("Menor de idade");
    }
}
```

## 🧠 Como Identificar Regras de Negócio?

Faça estas perguntas:
1. Isso muda se o sistema for para outro país? (Sim = regra)
2. Um dono de loja entenderia isso? (Sim = regra)
3. Um programador de outra linguagem não entenderia? (Não = regra)

**Exemplo**:
```java
// REGRA (qualquer dono de loja entende)
if (produto.isPerecivel() && !temRefrigeracao) {
    cancelarVenda();
}

// TECNOLOGIA (só programador entende)
if (produtoDAO.buscarPorId(id).getClass() == Perecivel.class) {
    entityManager.flush();
}
```

## 🏆 Boas Práticas para Regras de Negócio

1. **Separe sempre**:
   - Regras em classes como `ClienteService`, `VendaService`
   - Tecnologia em classes como `ClienteRepository`, `EmailSender`

2. **Dê nomes que um dono de loja entenderia**:
   - `aplicarDescontoAniversario()` ✅
   - `processarCodigo123()` ❌

3. **Teste separadamente**:
   ```java
   @Test
   void descontoMaiorQue20Reais() {
       VendaService service = new VendaService();
       BigDecimal resultado = service.calcularDesconto(new BigDecimal("25"));
       assertEquals(new BigDecimal("2.5"), resultado);
   }
   ```

## 🔄 Exemplo Completo: Sistema de Biblioteca

### Regras de Negócio:
```java
@Service
public class BibliotecaService {
    
    // Regra 1: Empréstimo máximo de 5 livros
    public boolean podeEmprestar(Cliente cliente) {
        return cliente.getLivrosEmprestados() < 5;
    }
    
    // Regra 2: Multa por atraso = R$1 por dia
    public BigDecimal calcularMulta(Emprestimo emp) {
        long diasAtraso = ChronoUnit.DAYS.between(
            emp.getDataDevolucao(), 
            LocalDate.now()
        );
        return BigDecimal.valueOf(Math.max(0, diasAtraso));
    }
    
    // Regra 3: Reservar livro por 48h
    public boolean reservaExpirada(Reserva reserva) {
        return reserva.getDataReserva()
                     .isBefore(LocalDateTime.now().minusHours(48));
    }
}
```

### Tecnologia (Spring Data JPA):
```java
@Repository
public interface EmprestimoRepository extends JpaRepository<Emprestimo, Long> {
    // Consultas técnicas ao banco
    List<Emprestimo> findByClienteAndDataDevolucaoIsNull(Cliente c);
}
```

## 🎯 Dicas para Iniciantes

1. **Sempre pergunte**: "Isso é sobre como a loja funciona ou sobre como o computador faz?"
   - Loja = Regra de Negócio
   - Computador = Tecnologia

2. **Comece simples**:
   ```java
   // Versão 1: Direto no Controller
   @PostMapping("/venda")
   public ResponseEntity<?> vender(@RequestBody VendaDTO dto) {
       if (dto.getIdade() < 18) {  // Regra aqui mesmo
           return ResponseEntity.badRequest().build();
       }
       // ...
   }
   
   // Versão 2: Extraindo para Service
   @Service
   public class VendaService {
       public void validarIdade(int idade) {
           if (idade < 18) throw new RegraNegocioException(...);
       }
   }
   ```

3. **Evolua para padrões avançados**:
   ```java
   // Domain-Driven Design (DDD)
   public class Cliente {
       private int idade;
       
       public void fazerAniversario() {
           this.idade++;
           if (this.idade == 18) {
               DomainEvents.publish(new ClienteMaioridadeEvent(this));
           }
       }
   }
   ```

Lembre-se: regras de negócio são como as leis do seu país - elas dizem o que pode e não pode no seu sistema! 🇧🇷✨