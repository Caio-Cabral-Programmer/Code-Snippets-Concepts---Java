# **🌱 Spring Core para Iniciantes em Java: Guia Detalhado**

Spring Core é o **alicerce fundamental** do ecossistema Spring, responsável pelas funcionalidades mais básicas e essenciais do framework. Vamos explorá-lo de forma didática, com exemplos práticos e conceitos claros.

## **📌 O que é o Spring Core?**
É o módulo central do Spring que fornece:
- **Container de Inversão de Controle (IoC)**: Gerencia objetos Java (beans) e suas dependências
- **Injeção de Dependências (DI)**: Mecanismo para fornecer dependências aos objetos
- **Gerenciamento do Ciclo de Vida** dos beans
- **Acesso a recursos** (arquivos, URLs, etc.)

## **🛠 Componentes Principais**

### **1. Container IoC**
O "cérebro" do Spring que gerencia seus objetos. Existem dois tipos principais:
- **BeanFactory** (interface básica)
- **ApplicationContext** (mais completo, o que usamos normalmente)

```java
// Exemplo de criação manual do container
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
```

### **2. Beans**
São os objetos gerenciados pelo Spring. Podem ser qualquer classe Java anotada ou declarada em configuração.

### **3. Configuração**
Há três formas de configurar o Spring Core:

| Método                | Como Funciona                              | Exemplo                          |
|-----------------------|-------------------------------------------|----------------------------------|
| **XML**              | Configuração via arquivos XML             | `<bean id="servico" class="com.exemplo.Servico"/>` |
| **Anotações**        | Usa anotações nas classes                 | `@Component`, `@Service`         |
| **Java Config**      | Configuração via classes Java             | `@Configuration`, `@Bean`        |

## **🔍 Funcionamento Passo a Passo**

1. **Definição dos Beans**: Você diz ao Spring quais classes devem ser gerenciadas
2. **Configuração**: Define como esses beans se relacionam (dependências)
3. **Inicialização**: O container Spring é iniciado
4. **Execução**: O Spring gerencia os objetos e suas dependências

## **💻 Exemplo Prático com Anotações**

### **1. Configuração Básica**
```java
@Configuration  // Indica que esta classe contém configurações do Spring
@ComponentScan("com.exemplo")  // Onde procurar por componentes
public class AppConfig {
    // Configurações adicionais podem ser feitas aqui
}
```

### **2. Definindo um Service**
```java
@Service  // Marca esta classe como um bean gerenciado pelo Spring
public class PedidoService {
    private final PedidoRepository repository;

    @Autowired  // Injeção de dependência via construtor
    public PedidoService(PedidoRepository repository) {
        this.repository = repository;
    }

    public void processarPedido(String pedido) {
        repository.salvar(pedido);
    }
}
```

### **3. Definindo um Repository**
```java
@Repository  // Indica que é um bean de acesso a dados
public class PedidoRepository {
    public void salvar(String pedido) {
        System.out.println("Pedido salvo: " + pedido);
    }
}
```

### **4. Usando a Aplicação**
```java
public class MainApp {
    public static void main(String[] args) {
        // 1. Inicializa o container Spring
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        
        // 2. Obtém o bean do Service
        PedidoService service = context.getBean(PedidoService.class);
        
        // 3. Usa o serviço
        service.processarPedido("Notebook Dell");
    }
}
```

## **🎯 Conceitos-Chave Explicados**

### **1. Ciclo de Vida dos Beans**
O Spring gerencia todo o ciclo de vida dos beans:
1. **Instanciação**: Cria o objeto
2. **Injeção de Dependências**: Preenche as dependências
3. **Inicialização**: Chama métodos de callback como `@PostConstruct`
4. **Uso**: Bean está pronto para ser usado
5. **Destruição**: Chama métodos de cleanup como `@PreDestroy`

### **2. Escopos de Beans**
Define o tempo de vida e visibilidade dos beans:

| Escopo          | Descrição                                  |
|-----------------|-------------------------------------------|
| **singleton**   | Uma única instância por container (padrão) |
| **prototype**   | Nova instância a cada requisição           |
| **request**     | Uma instância por requisição HTTP          |
| **session**     | Uma instância por sessão HTTP              |
| **application** | Uma instância por contexto Servlet         |

Exemplo de definição:
```java
@Bean
@Scope("prototype")
public MeuBean meuBean() {
    return new MeuBean();
}
```

### **3. Injeção de Dependências**
Três formas principais:

**Por Construtor (Recomendado):**
```java
@Service
public class PedidoService {
    private final PedidoRepository repository;

    @Autowired
    public PedidoService(PedidoRepository repository) {
        this.repository = repository;
    }
}
```

**Por Setter:**
```java
@Service
public class PedidoService {
    private PedidoRepository repository;

    @Autowired
    public void setRepository(PedidoRepository repository) {
        this.repository = repository;
    }
}
```

**Por Campo (Evitar):**
```java
@Service
public class PedidoService {
    @Autowired
    private PedidoRepository repository;
}
```

## **🔄 XML vs Anotações vs Java Config**

### **Configuração via XML**
```xml
<beans>
    <bean id="pedidoRepository" class="com.exemplo.PedidoRepository"/>
    <bean id="pedidoService" class="com.exemplo.PedidoService">
        <constructor-arg ref="pedidoRepository"/>
    </bean>
</beans>
```

### **Configuração via Java**
```java
@Configuration
public class AppConfig {
    @Bean
    public PedidoRepository pedidoRepository() {
        return new PedidoRepository();
    }

    @Bean
    public PedidoService pedidoService() {
        return new PedidoService(pedidoRepository());
    }
}
```

## **🔧 Ferramentas Úteis**

1. **@PostConstruct e @PreDestroy**: Para inicialização e limpeza
   ```java
   @Repository
   public class PedidoRepository {
       @PostConstruct
       public void init() {
           System.out.println("Bean inicializado!");
       }
       
       @PreDestroy
       public void cleanup() {
           System.out.println("Bean sendo destruído!");
       }
   }
   ```

2. **@Primary**: Para resolver ambiguidades quando há múltiplas implementações
   ```java
   @Repository @Primary
   public class MeuRepositorio implements Repositorio {
       // implementação
   }
   ```

3. **@Qualifier**: Para especificar qual bean injetar
   ```java
   @Autowired
   @Qualifier("meuRepositorioEspecial")
   private Repositorio repositorio;
   ```

## **🚀 Boas Práticas com Spring Core**

1. **Prefira injeção por construtor**: Mais testável e imutável
2. **Use interfaces para dependências**: Facilita mudanças de implementação
3. **Evite anotações @Autowired em campos**: Dificulta testes
4. **Organize seus pacotes logicamente**: Facilita o @ComponentScan
5. **Documente seus beans**: Use @Description ou JavaDoc

## **📚 Evoluindo no Spring Core**

Depois de dominar o básico, explore:
- **Spring Expression Language (SpEL)**
- **Eventos e Listeners** do Spring
- **Custom scopes**
- **BeanFactoryPostProcessor**
- **FactoryBeans**

O Spring Core é a base para todos os outros módulos Spring. Dominá-lo é essencial para trabalhar eficientemente com Spring Boot, Spring MVC, Spring Data e outros.

Quer mergulhar em algum tópico específico do Spring Core com mais detalhes? Posso elaborar exemplos mais avançados! 😊