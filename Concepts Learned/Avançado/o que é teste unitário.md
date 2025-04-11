**Teste unitário** é uma prática de desenvolvimento de software onde pequenas partes do código, chamadas de **unidades**, são testadas de forma isolada para garantir que funcionem corretamente. Uma unidade pode ser uma função, um método, uma classe ou até mesmo um pequeno conjunto de classes que trabalham juntas para realizar uma tarefa específica.

O objetivo principal dos testes unitários é **validar a lógica do código** e garantir que cada parte do sistema funcione conforme o esperado, antes de integrá-la com outras partes do sistema.

---

### Características dos testes unitários:
1. **Isolamento**:
   - O teste unitário deve ser independente de outras partes do sistema.
   - Dependências externas (como bancos de dados, APIs ou serviços) são substituídas por **mocks** ou **stubs** (simulações).

2. **Automatizado**:
   - Testes unitários são escritos em código e podem ser executados automaticamente, geralmente como parte de um processo de integração contínua (CI).

3. **Rápido**:
   - Como testam apenas pequenas partes do código, os testes unitários devem ser executados rapidamente.

4. **Repetível**:
   - O resultado de um teste unitário deve ser consistente, independentemente de quantas vezes ele é executado.

---

### Por que escrever testes unitários?
1. **Detectar bugs cedo**:
   - Problemas são identificados durante o desenvolvimento, antes que o código seja integrado ao sistema.

2. **Facilitar refatoração**:
   - Com testes unitários, você pode modificar o código com confiança, sabendo que os testes vão detectar se algo quebrar.

3. **Documentação viva**:
   - Testes unitários servem como exemplos de como o código deve ser usado e quais são seus comportamentos esperados.

4. **Melhorar a qualidade do código**:
   - Escrever testes unitários incentiva a criação de código modular e bem estruturado.

---

### Exemplo de teste unitário em Java
Vamos supor que você tenha uma classe simples chamada `Calculadora` com um método `somar`:

```java
public class Calculadora {
    public int somar(int a, int b) {
        return a + b;
    }
}
```

Um teste unitário para esse método pode ser escrito usando uma ferramenta como **JUnit** (a biblioteca de testes mais popular para Java):

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import org.junit.jupiter.api.Test;

public class CalculadoraTest {

    @Test
    public void testSomar() {
        Calculadora calculadora = new Calculadora();
        int resultado = calculadora.somar(2, 3);
        assertEquals(5, resultado); // Verifica se o resultado é 5
    }
}
```

#### O que esse teste faz?
1. Cria uma instância da classe `Calculadora`.
2. Chama o método `somar` com os valores `2` e `3`.
3. Verifica se o resultado é `5` usando o método `assertEquals`.

---

### Ferramentas comuns para testes unitários em Java
1. **JUnit**: A ferramenta mais popular para testes unitários em Java.
2. **TestNG**: Uma alternativa ao JUnit com funcionalidades adicionais.
3. **Mockito**: Usado para criar mocks e simular dependências externas.

---

### Boas práticas para testes unitários
1. **Teste um comportamento por vez**:
   - Cada teste deve verificar apenas uma funcionalidade específica.

2. **Use nomes descritivos**:
   - Nomes de testes devem descrever o comportamento que está sendo testado. Por exemplo, `testSomarDoisNumerosPositivos`.

3. **Mantenha os testes simples**:
   - Evite lógica complexa nos testes. Eles devem ser fáceis de entender e manter.

4. **Execute os testes frequentemente**:
   - Integre os testes unitários ao processo de build para garantir que sejam executados automaticamente.

---

### Resumo
- **Teste unitário** é a prática de testar pequenas partes do código de forma isolada.
- Ele ajuda a garantir que cada unidade do sistema funcione corretamente.
- Em Java, ferramentas como JUnit e Mockito são usadas para escrever e executar testes unitários.
- Testes unitários são essenciais para garantir a qualidade e a confiabilidade do código.

Se precisar de mais exemplos ou explicações, é só perguntar! 😊
