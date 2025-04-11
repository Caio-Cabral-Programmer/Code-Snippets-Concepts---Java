### **O que é um Mock? (Para Iniciantes em Java)**  

Em desenvolvimento de software, um **Mock** (ou *Mock Object*) é um objeto simulado que imita o comportamento de um objeto real em um ambiente controlado. Ele é usado principalmente em **testes unitários** para isolar o código que está sendo testado, evitando dependências externas (como bancos de dados, APIs ou serviços complexos).  

---

## **📌 Por que usar Mocks?**  
Imagine que você está testando uma classe que faz uma chamada a um banco de dados. Se você usar o banco real:  
- O teste pode ficar lento.  
- Dados podem ser alterados, afetando os resultados.  
- Pode ser difícil simular erros (como conexão falhando).  

Com um **Mock**, você substitui o banco de dados por um objeto falso que **simula** o comportamento esperado, tornando os testes:  
✅ **Rápidos** (não dependem de recursos externos).  
✅ **Confiáveis** (sempre retornam o que você definir).  
✅ **Isolados** (testam apenas a lógica da classe, sem efeitos colaterais).  

---

## **🛠 Exemplo Prático em Java (com Mockito)**  

Vamos supor que temos uma classe `ServicoDePagamento` que depende de uma classe `GatewayDePagamento` (que se comunica com um sistema externo).  

### **1. Classe Real (Sem Mock)**  
```java
public class ServicoDePagamento {
    private GatewayDePagamento gateway;

    public ServicoDePagamento(GatewayDePagamento gateway) {
        this.gateway = gateway;
    }

    public boolean processarPagamento(double valor) {
        // Chama o gateway real (pode ser lento e instável)
        return gateway.efetuarPagamento(valor);
    }
}
```

### **2. Teste Usando Mock (Com Mockito)**  
```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;

public class ServicoDePagamentoTest {

    @Test
    public void testeProcessarPagamentoComSucesso() {
        // 1. Cria um mock do GatewayDePagamento
        GatewayDePagamento gatewayMock = mock(GatewayDePagamento.class);

        // 2. Define o comportamento do mock
        when(gatewayMock.efetuarPagamento(100.0)).thenReturn(true);

        // 3. Injeta o mock no ServicoDePagamento
        ServicoDePagamento servico = new ServicoDePagamento(gatewayMock);

        // 4. Executa o teste
        boolean resultado = servico.processarPagamento(100.0);

        // 5. Verifica se funcionou
        assertTrue(resultado);

        // 6. (Opcional) Verifica se o método foi chamado
        verify(gatewayMock).efetuarPagamento(100.0);
    }
}
```

---

## **📌 Principais Conceitos**  

### **1. `mock()`**  
Cria um objeto falso da classe especificada.  

### **2. `when().thenReturn()`**  
Define qual comportamento o mock deve ter quando um método é chamado.  
```java
when(gatewayMock.efetuarPagamento(100.0)).thenReturn(true);
// Quando "efetuarPagamento(100.0)" for chamado, retorne "true".
```

### **3. `verify()`**  
Verifica se um método do mock foi chamado conforme esperado.  
```java
verify(gatewayMock).efetuarPagamento(100.0); // Garante que o método foi chamado.
```

---

## **🔄 Quando Usar Mocks?**  
- Testar classes que dependem de **bancos de dados, APIs ou serviços externos**.  
- Simular **comportamentos complexos** (ex.: "e se o pagamento falhar?").  
- Evitar **efeitos colaterais** em testes (ex.: enviar e-mails reais durante testes).  

---

## **📚 Bibliotecas Populares para Mock em Java**  
1. **Mockito** (a mais usada, simples e poderosa).  
2. **EasyMock** (alternativa mais antiga).  
3. **JMockit** (mais avançado, mas menos intuitivo).  

---

## **🎯 Resumo**  
✔ **Mock** = Objeto falso que simula comportamentos controlados.  
✔ **Usado em testes** para isolar dependências externas.  
✔ **Mockito** é a biblioteca mais comum para criar mocks em Java.  
✔ **`when().thenReturn()`** define o comportamento, **`verify()`** confirma chamadas.  

Se você está começando, experimente criar um teste simples com **Mockito** e veja como os mocks ajudam a testar seu código de forma limpa e eficiente! 🚀  

Quer um exemplo mais específico? Posso te mostrar um caso com **banco de dados mockado** ou **API REST falsa**! 😊