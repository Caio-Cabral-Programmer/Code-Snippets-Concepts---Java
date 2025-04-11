# 🌱 **Introdução ao Spring Framework para Iniciantes em Java**  

O **Spring** é um dos frameworks mais populares para desenvolvimento de aplicações Java. Ele simplifica a criação de sistemas robustos, modulares e escaláveis, seguindo boas práticas como **Inversão de Controle (IoC)** e **Injeção de Dependências (DI)**.  

Vamos aprender de forma **didática e prática**!  

---

## **📌 O que é o Spring Framework?**  
O Spring é um **framework open-source** que fornece infraestrutura para desenvolver aplicações Java de forma mais fácil e organizada. Ele é modular, ou seja, você pode usar apenas as partes que precisar.  

### **Principais vantagens:**  
✅ **Facilita o desenvolvimento** (menos código repetitivo).  
✅ **Promove boas práticas** (como desacoplamento e testes).  
✅ **Oferece módulos para quase tudo** (web, segurança, banco de dados, etc.).  

---

## **🛠 Principais Módulos do Spring**  

| Módulo                | Para que serve? |
|-----------------------|----------------|
| **Spring Core**       | Funcionalidades básicas (IoC, DI). |
| **Spring MVC**        | Cria aplicações web (controllers, REST APIs). |
| **Spring Boot**       | Autoconfiguração para projetos rápidos. |
| **Spring Data**       | Simplifica acesso a bancos de dados (JPA, MongoDB). |
| **Spring Security**   | Autenticação e autorização em aplicações. |
| **Spring Cloud**      | Desenvolvimento de microsserviços. |

---

## **🎯 Conceitos Fundamentais**  

### **1. Inversão de Controle (IoC) e Injeção de Dependência (DI)**  
O Spring gerencia os objetos da aplicação (**beans**) em um **container IoC**. Em vez de você criar objetos manualmente (`new Servico()`), o Spring os injeta onde são necessários.  

#### **Exemplo SEM Spring:**  
```java
public class PedidoService {
    private PedidoRepository repository = new PedidoRepository(); // Acoplamento forte!
    
    public void salvarPedido(Pedido pedido) {
        repository.save(pedido);
    }
}
```  

#### **Exemplo COM Spring (usando DI):**  
```java
@Service // Indica que é um serviço gerenciado pelo Spring
public class PedidoService {
    @Autowired // Spring injeta automaticamente
    private PedidoRepository repository;
    
    public void salvarPedido(Pedido pedido) {
        repository.save(pedido);
    }
}
```  

### **2. Anotações Principais**  
| Anotação          | O que faz? |
|-------------------|------------|
| `@Component`      | Define uma classe como gerenciada pelo Spring. |
| `@Service`        | Indica um serviço (lógica de negócio). |
| `@Repository`     | Classe que acessa banco de dados. |
| `@Controller` / `@RestController` | Lida com requisições web (MVC/REST). |
| `@Autowired`      | Injeta dependências automaticamente. |

---

## **🚀 Spring Boot: Simplificando o Spring**  
O **Spring Boot** é uma extensão do Spring que:  
✔ **Configura automaticamente** a aplicação.  
✔ **Tem servidor embutido** (Tomcat, Jetty).  
✔ **Facilita criação de APIs REST** com `@RestController`.  

### **Exemplo de API REST com Spring Boot:**  
```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Olá, Spring Boot!";
    }
}
```  
Ao executar, acesse: [`http://localhost:8080/hello`](http://localhost:8080/hello)  

---

## **🔧 Como Começar?**  
1. **Instale o Spring Boot:**  
   - Crie um projeto em [start.spring.io](https://start.spring.io/) (adicione dependências como `Spring Web`).  
   - Ou use uma IDE (IntelliJ, Eclipse) com suporte a Spring.  

2. **Estrutura Básica:**  
   ```
   src/
   ├── main/
   │   ├── java/
   │   │   └── com/exemplo/MinhaAplicacao.java (classe principal)
   │   └── resources/
   │       ├── application.properties (configurações)
   └── test/ (testes automatizados)
   ```

3. **Rode a Aplicação:**  
   - Execute `MinhaAplicacao.java` (contém `@SpringBootApplication`).  

---

## **📚 Aprofundando**  
- **Spring Data JPA:** Para trabalhar com bancos de dados.  
  ```java
  @Repository
  public interface UsuarioRepository extends JpaRepository<Usuario, Long> {
      // Métodos automáticos: save(), findAll(), findById(), etc.
  }
  ```  

- **Spring Security:** Para autenticação.  
  ```java
  @Configuration
  public class SecurityConfig extends WebSecurityConfigurerAdapter {
      @Override
      protected void configure(HttpSecurity http) throws Exception {
          http.authorizeRequests().anyRequest().authenticated();
      }
  }
  ```  

---

## **🎯 Resumo**  
✔ **Spring** = Framework Java para aplicações robustas e organizadas.  
✔ **IoC/DI** = O Spring gerencia e injeta dependências automaticamente.  
✔ **Spring Boot** = Facilita a criação de projetos Spring.  
✔ **Anotações** = `@Component`, `@Service`, `@Autowired`, etc., simplificam o desenvolvimento.  

Quer um exemplo **passo a passo** de como criar uma **API REST com Spring Boot + Banco de Dados**? Posso te guiar! 😊  

**Dica:** Comece com um projeto simples (ex.: uma API de lista de tarefas) e evolua aos poucos! 🚀