# **🌱 Inversão de Controle (IoC) para Iniciantes em Java**  

A **Inversão de Controle (IoC)** é um **princípio de design de software** que transfere a responsabilidade de gerenciar objetos e dependências de um programa **para um container/framework externo** (como o **Spring**).  

Em termos simples:  
🔹 **SEM IoC:** Seu código controla a criação e o gerenciamento de objetos.  
🔹 **COM IoC:** Um **container (como o Spring)** cuida disso para você, seguindo regras pré-definidas.  

---

## **📌 Problema que o IoC Resolve**  
Imagine que você tem uma classe `PedidoService` que depende de `PedidoRepository` para salvar dados no banco:  

### **Versão SEM IoC (Acoplamento Forte)**  
```java
public class PedidoService {
    // A classe PedidoService cria sua própria dependência (problema!)
    private PedidoRepository repository = new PedidoRepository(); 

    public void salvarPedido(Pedido pedido) {
        repository.salvar(pedido);
    }
}
```  
**Problemas:**  
❌ Dificulta testes (não podemos substituir `PedidoRepository` por um mock).  
❌ Se `PedidoRepository` mudar, `PedidoService` precisa ser alterado.  
❌ Controle está **nas mãos da classe**, não flexível.  

---

## **🔄 Solução: IoC (Inversão de Controle)**  
Com IoC, **o controle é invertido**:  
- O **container (Spring)** cria e injeta as dependências.  
- Suas classes **não instanciam dependências diretamente**, apenas as recebem.  

### **Versão COM IoC (Usando Spring)**  
```java
public class PedidoService {
    // A dependência é INJETADA pelo Spring (não criada aqui)
    private PedidoRepository repository;

    // Construtor recebe a dependência (Injeção por Construtor)
    public PedidoService(PedidoRepository repository) {
        this.repository = repository;
    }

    public void salvarPedido(Pedido pedido) {
        repository.salvar(pedido);
    }
}
```  
**Vantagens:**  
✅ **Flexibilidade:** Podemos passar diferentes implementações de `PedidoRepository`.  
✅ **Testabilidade:** Fácil substituir `PedidoRepository` por um **Mock** em testes.  
✅ **Desacoplamento:** `PedidoService` não sabe como `PedidoRepository` é criado.  

---

## **🎯 Como o IoC Funciona no Spring?**  
O Spring usa um **Container IoC** que:  
1. **Descobre** quais classes devem ser gerenciadas (usando anotações como `@Component`, `@Service`).  
2. **Cria os objetos** (chamados de **beans**) e resolve suas dependências.  
3. **Injeta** as dependências onde são necessárias (via `@Autowired` ou construtor).  

### **Exemplo com Anotações:**  
```java
@Service // Indica que o Spring deve gerenciar esta classe
public class PedidoService {
    private PedidoRepository repository;

    @Autowired // O Spring injeta automaticamente
    public PedidoService(PedidoRepository repository) {
        this.repository = repository;
    }
}
```  

```java
@Repository // Indica que é um repositório gerenciado pelo Spring
public class PedidoRepository {
    public void salvar(Pedido pedido) {
        System.out.println("Salvando pedido...");
    }
}
```  

---

## **🔹 Tipos de Injeção de Dependência (DI)**  
A IoC é implementada via **Injeção de Dependência (DI)**. Os 3 principais tipos são:  

### **1. Injeção por Construtor (Recomendada)**  
```java
@Service
public class PedidoService {
    private final PedidoRepository repository;

    // O Spring injeta via construtor
    public PedidoService(PedidoRepository repository) {
        this.repository = repository;
    }
}
```  

### **2. Injeção por Setter**  
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

### **3. Injeção por Campo (Não recomendado para testes)**  
```java
@Service
public class PedidoService {
    @Autowired // Injeção direta no campo (evitar em código novo)
    private PedidoRepository repository;
}
```  

---

## **📌 Resumo: IoC vs DI**  
| **Inversão de Controle (IoC)** | **Injeção de Dependência (DI)** |  
|-------------------------------|--------------------------------|  
| Princípio que **inverte o controle** de criação de objetos. | **Implementação prática** do IoC (como as dependências são injetadas). |  
| O **container (Spring)** gerencia o ciclo de vida dos objetos. | Pode ser feita por **construtor, setter ou campo**. |  

---

## **🚀 Por que IoC é Importante?**  
✔ **Reduz acoplamento:** Classes não dependem de implementações concretas.  
✔ **Facilita testes:** Dependências podem ser mockadas.  
✔ **Torna o código mais modular e sustentável.**  

---

## **💡 Exemplo Prático Completo**  
Veja um exemplo funcional com Spring Boot:  

### **Classe Principal**  
```java
@SpringBootApplication
public class MainApp {
    public static void main(String[] args) {
        SpringApplication.run(MainApp.class, args);
    }
}
```  

### **Serviço + Repositório**  
```java
@Service
public class PedidoService {
    private final PedidoRepository repository;

    public PedidoService(PedidoRepository repository) {
        this.repository = repository;
    }

    public void processarPedido(String produto) {
        repository.salvar(produto);
    }
}
```  

```java
@Repository
public class PedidoRepository {
    public void salvar(String produto) {
        System.out.println("Pedido salvo: " + produto);
    }
}
```  

### **Testando**  
```java
@SpringBootTest
public class PedidoServiceTest {
    @Autowired
    private PedidoService pedidoService;

    @Test
    public void testProcessarPedido() {
        pedidoService.processarPedido("Notebook");
        // Verifica se o pedido foi processado
    }
}
```  

---

## **🎯 Conclusão**  
- **IoC** = O framework (Spring) controla a criação e injeção de dependências.  
- **DI** = Forma como as dependências são fornecidas (construtor, setter, campo).  
- **Benefícios:** Código mais testável, flexível e organizado.  

Quer ver um **exemplo com banco de dados real** ou **como usar IoC em testes com Mockito**? Posso explicar! 😊