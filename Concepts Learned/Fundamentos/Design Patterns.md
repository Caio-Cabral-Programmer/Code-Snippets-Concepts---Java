# Design Patterns em Java - Guia para Iniciantes

Design Patterns (Padrões de Projeto) são soluções **testadas e comprovadas** para problemas comuns de design de software. Vamos explorar esse conceito fundamental de forma didática.

## 1. O que são Design Patterns?

São como "receitas" ou "modelos" que:
- Solucionam problemas recorrentes no desenvolvimento de software
- Fornecem melhores práticas de organização de código
- Facilitam a comunicação entre desenvolvedores ("Vamos usar um Singleton aqui")

## 2. Por que usar?

- Evita "reinventar a roda" para problemas conhecidos
- Promove código mais limpo e organizado
- Facilita manutenção e extensão do código
- Melhora a comunicação técnica

## 3. Tipos Principais de Design Patterns

Existem 23 padrões clássicos, divididos em 3 categorias:

### A) Padrões Criacionais (Criação de objetos)
- **Singleton**: Garante uma única instância de uma classe
- **Factory Method**: Cria objetos sem especificar a classe concreta
- **Builder**: Construção complexa de objetos passo a passo

### B) Padrões Estruturais (Composição de classes/objetos)
- **Adapter**: Permite interfaces incompatíveis trabalharem juntas
- **Decorator**: Adiciona responsabilidades dinamicamente
- **Facade**: Fornece uma interface simplificada para um subsistema complexo

### C) Padrões Comportamentais (Comunicação entre objetos)
- **Observer**: Notifica mudanças a múltiplos objetos
- **Strategy**: Permite variar algoritmos independentemente dos clientes
- **Command**: Encapsula uma solicitação como um objeto

## 4. Exemplos Detalhados

### Singleton (Criacional)
Garante uma única instância de uma classe:

```java
public class Database {
    private static Database instance;
    
    private Database() {} // Construtor privado
    
    public static Database getInstance() {
        if (instance == null) {
            instance = new Database();
        }
        return instance;
    }
    
    // Métodos da classe...
}

// Uso:
Database db = Database.getInstance();
```

### Factory Method (Criacional)
Cria objetos sem especificar a classe concreta:

```java
interface Animal {
    void fazerSom();
}

class Cachorro implements Animal {
    public void fazerSom() { System.out.println("Au au!"); }
}

class AnimalFactory {
    public Animal criarAnimal(String tipo) {
        if ("cachorro".equalsIgnoreCase(tipo)) {
            return new Cachorro();
        }
        // outros animais...
        return null;
    }
}

// Uso:
Animal meuPet = new AnimalFactory().criarAnimal("cachorro");
meuPet.fazerSom(); // Au au!
```

### Observer (Comportamental)
Notifica objetos sobre mudanças:

```java
import java.util.ArrayList;
import java.util.List;

interface Observador {
    void atualizar(String mensagem);
}

class Assunto {
    private List<Observador> observadores = new ArrayList<>();
    
    public void adicionarObservador(Observador o) {
        observadores.add(o);
    }
    
    public void notificarTodos(String mensagem) {
        for (Observador o : observadores) {
            o.atualizar(mensagem);
        }
    }
}

// Uso:
Assunto assunto = new Assunto();
assunto.adicionarObservador(mensagem -> System.out.println("Observador 1: " + mensagem));
assunto.notificarTodos("Mudança ocorrida!");
```

## 5. Como Aprender Design Patterns?

1. **Entenda o problema** que o padrão resolve
2. **Estude a estrutura** básica do padrão
3. **Implemente exemplos simples** em Java
4. **Identifique casos reais** onde aplicá-los
5. **Comece com os mais usados**:
   - Singleton
   - Factory Method
   - Observer
   - Strategy
   - Decorator

## 6. Benefícios no Mundo Real

- **Singleton**: Conexão com banco de dados
- **Factory**: Criação de diferentes tipos de documentos
- **Observer**: Sistemas de notificação
- **Strategy**: Algoritmos de pagamento (cartão, boleto, pix)

## 7. Cuidados Importantes

- Não force o uso de padrões onde não são necessários
- Evite over-engineering (soluções complexas demais para problemas simples)
- Priorize a clareza do código sobre o uso de padrões

## 8. Próximos Passos

1. Pratique implementando os padrões básicos
2. Explore bibliotecas do Java que usam padrões:
   - `java.util.Collections#sort()` (Strategy)
   - `java.io` (Decorator)
3. Estude o livro clássico "Design Patterns" (Gang of Four)

Lembre-se: Design Patterns são ferramentas, não objetivos em si mesmos. Use-os para escrever código mais limpo, flexível e mantenível!