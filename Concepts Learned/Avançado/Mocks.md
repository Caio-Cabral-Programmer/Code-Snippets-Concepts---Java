# **Mocks para Iniciantes (Explicação Detalhada e Didática)**  

Olá, futuro(a) programador(a)! 👋 Hoje vamos falar sobre **Mocks**—uma técnica superpoderosa para testar código sem depender de coisas reais (como bancos de dados, APIs ou serviços externos). Vou explicar como se você fosse uma criança, com exemplos fáceis e sem pular nada. Vamos começar!  

---

## **1. O Que São Mocks? (Exemplo do Mundo Real)**  

Imagine que você está brincando de **restaurante** 🍔 com seus amigos:  
- Você é o **chef** (seu programa).  
- Seu amigo é o **garçom** (um serviço externo, como um banco de dados).  

Mas e se o garçom **não estiver disponível**? Como você testa se o chef está preparando o lanche certo?  

👉 **Solução:** Você usa um **garçom de mentira (mock)** que **finge** ser o garçom real, mas só simula as respostas.  

No código, **mocks** são **objetos falsos** que imitam comportamentos reais para testar seu código **isoladamente**.  

---

## **2. Por Que Usar Mocks?**  

### **Problema sem Mocks (Modo Arcaico)**  
Suponha que temos uma classe `PagamentoService` que depende de um `BancoDeDadosReal`:  

```java
class PagamentoService {
    private BancoDeDadosReal bancoDeDados; // Dependência concreta (ruim para testes)

    public PagamentoService() {
        this.bancoDeDados = new BancoDeDadosReal(); // Problema: e se o banco estiver offline?
    }

    public boolean processarPagamento(int valor) {
        if (bancoDeDados.temSaldo(valor)) {
            bancoDeDados.debitar(valor);
            return true;
        }
        return false;
    }
}
```

**Problemas:**  
❌ Se o banco de dados **não estiver disponível**, o teste quebra.  
❌ Testes ficam **lentos** (precisam de conexão real).  
❌ Dificuldade de testar **casos extremos** (ex.: "e se o banco lançar um erro?").  

---

### **Solução com Mocks (Modo Moderno)**  
Vamos refatorar usando **inversão de dependência** (DIP) e **mocks**:  

#### **Passo 1: Criar uma Interface (Abstração)**  
```java
interface BancoDeDados {
    boolean temSaldo(int valor);
    void debitar(int valor);
}
```

#### **Passo 2: Implementação Real (Banco de Dados Verdadeiro)**  
```java
class BancoDeDadosReal implements BancoDeDados {
    public boolean temSaldo(int valor) {
        // Consulta SQL real (demorado)
        return valor <= 1000; // Exemplo simplificado
    }

    public void debitar(int valor) {
        System.out.println("Debitando R$" + valor + " do banco real...");
    }
}
```

#### **Passo 3: Implementação Fake (Mock para Testes)**  
```java
class BancoDeDadosMock implements BancoDeDados {
    private boolean saldoDisponivel; // Controlamos o comportamento

    public BancoDeDadosMock(boolean saldoDisponivel) {
        this.saldoDisponivel = saldoDisponivel;
    }

    public boolean temSaldo(int valor) {
        return saldoDisponivel; // Retorna o que definirmos
    }

    public void debitar(int valor) {
        System.out.println("[MOCK] Simulando débito de R$" + valor);
    }
}
```

#### **Passo 4: Usar no `PagamentoService` (Com Injeção de Dependência)**  
```java
class PagamentoService {
    private BancoDeDados bancoDeDados; // Dependência da interface

    public PagamentoService(BancoDeDados bancoDeDados) {
        this.bancoDeDados = bancoDeDados;
    }

    public boolean processarPagamento(int valor) {
        if (bancoDeDados.temSaldo(valor)) {
            bancoDeDados.debitar(valor);
            return true;
        }
        return false;
    }
}
```

#### **Passo 5: Testando com Mocks**  
```java
public class TestePagamento {
    public static void main(String[] args) {
        // Cenário 1: Saldo suficiente (mock retorna true)
        BancoDeDados mockComSaldo = new BancoDeDadosMock(true);
        PagamentoService service1 = new PagamentoService(mockComSaldo);
        System.out.println(service1.processarPagamento(500)); // true

        // Cenário 2: Sem saldo (mock retorna false)
        BancoDeDados mockSemSaldo = new BancoDeDadosMock(false);
        PagamentoService service2 = new PagamentoService(mockSemSaldo);
        System.out.println(service2.processarPagamento(500)); // false
    }
}
```

**Vantagens:**  
✅ Testes **rápidos** (não dependem de banco real).  
✅ Testes **confiáveis** (controlamos o comportamento do mock).  
✅ Podemos simular **erros** (ex.: "e se o banco der timeout?").  

---

## **3. Mocks Manuais vs Frameworks (Mockito, EasyMock)**  

### **Modo Manual (Como Fizemos Acima)**  
- Criamos uma classe `BancoDeDadosMock` manualmente.  
- Funciona, mas **dá mais trabalho**.  

### **Modo Moderno (Usando Mockito - Framework de Mock Mais Popular em Java)**  
```java
import static org.mockito.Mockito.*;

public class TestePagamentoComMockito {
    public static void main(String[] args) {
        // 1. Cria um mock automaticamente
        BancoDeDados bancoMock = mock(BancoDeDados.class);

        // 2. Define comportamentos
        when(bancoMock.temSaldo(500)).thenReturn(true); // "Quando chamar temSaldo(500), retorne true"
        when(bancoMock.temSaldo(1001)).thenReturn(false); // "Se for 1001, retorne false"

        // 3. Testa o serviço
        PagamentoService service = new PagamentoService(bancoMock);
        System.out.println(service.processarPagamento(500)); // true
        System.out.println(service.processarPagamento(1001)); // false

        // 4. Verifica se o método foi chamado
        verify(bancoMock).debitar(500); // "Verifique se debitar(500) foi chamado"
    }
}
```

**Vantagens do Mockito:**  
🔥 Não precisa criar classes mock manualmente.  
🔥 Sintaxe mais limpa (`when(...).thenReturn(...)`).  
🔥 Pode verificar **quantas vezes um método foi chamado**.  

---

## **4. Quando Usar Mocks?**  

| **Caso de Uso**              | **Exemplo**                          | **Por Que Usar Mock?** |
|-----------------------------|-------------------------------------|-----------------------|
| **Testar serviços externos** | Banco de dados, API REST            | Evita dependência de sistemas reais (que podem falhar) |
| **Simular erros**           | "E se a API retornar erro 500?"     | Testa como seu código lida com falhas |
| **Testes unitários rápidos** | Validar lógica de negócios          | Roda em milissegundos (sem I/O) |
| **Evitar efeitos colaterais** | Não queremos debitar dinheiro de verdade | O mock só simula, não executa ações reais |

---

## **5. Resumo Final (Para Nunca Esquecer)**  

| **Conceito**          | **Sem Mocks**                     | **Com Mocks**                          |
|-----------------------|----------------------------------|---------------------------------------|
| **Dependência**       | Objetos reais (lentos, instáveis) | Objetos falsos (controláveis)         |
| **Velocidade**        | Testes lentos (com I/O real)      | Testes rápidos (tudo em memória)      |
| **Controle**          | Difícil simular casos extremos    | Facilidade de simular qualquer cenário |
| **Frameworks**        | Nenhum (código manual)            | Mockito, EasyMock, JMock              |

**Regras de Ouro para Mocks:**  
🔹 **Use para isolar testes** (não depender de sistemas externos).  
🔹 **Não mocke tudo!** Só o que é lento/externo.  
🔹 **Prefira frameworks como Mockito** (menos código manual).  

---

## **6. Exercício Prático**  

Que tal praticar? Crie uma classe `EmailService` que depende de um `ServicoDeEmailReal`. Depois:  
1. Crie uma interface `ServicoDeEmail`.  
2. Faça um mock manual (`ServicoDeEmailMock`).  
3. Teste com Mockito.  

Exemplo:  
```java
interface ServicoDeEmail {
    boolean enviar(String destinatario, String mensagem);
}

class EmailService {
    private ServicoDeEmail servico;

    public EmailService(ServicoDeEmail servico) {
        this.servico = servico;
    }

    public boolean enviarMensagem(String user, String msg) {
        return servico.enviar(user, msg);
    }
}
```

**Desafio:**  
- Teste um caso onde `enviar()` retorna `true`.  
- Teste um caso onde `enviar()` retorna `false`.  
- Use Mockito para verificar se `enviar()` foi chamado.  

---

Espero que tenha entendido! Agora você já pode testar seu código como um profissional. 🚀  

Bons estudos! 😊