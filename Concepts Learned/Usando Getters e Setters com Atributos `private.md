# **Usando Getters e Setters com Atributos `private`**

Sim, exatamente! Essa é uma das **melhores práticas** em Java (e na Programação Orientada a Objetos em geral). Vamos explicar detalhadamente:

## **Por Que Usar Getters/Setters com `private`?**

1. **Encapsulamento**: Você protege os dados internos da classe
2. **Controle**: Pode validar ou processar valores antes de atribuir
3. **Flexibilidade**: Pode mudar a implementação interna sem afetar quem usa a classe
4. **Segurança**: Evita modificações indevidas diretas nos atributos

## **Exemplo Prático**

```java
public class Pessoa {
    // Atributo PRIVATE (acessível só dentro da classe)
    private String nome;
    private int idade;

    // GETTER (método público para LEITURA)
    public String getNome() {
        return this.nome;
    }

    // SETTER (método público para ESCRITA)
    public void setNome(String novoNome) {
        if (novoNome == null || novoNome.isEmpty()) {
            throw new IllegalArgumentException("Nome inválido!");
        }
        this.nome = novoNome;
    }

    // Getter para idade
    public int getIdade() {
        return this.idade;
    }

    // Setter com validação
    public void setIdade(int novaIdade) {
        if (novaIdade < 0 || novaIdade > 120) {
            throw new IllegalArgumentException("Idade deve ser entre 0 e 120");
        }
        this.idade = novaIdade;
    }
}
```

## **Como Usar na Prática**

```java
public class Main {
    public static void main(String[] args) {
        Pessoa p = new Pessoa();
        
        p.setNome("João"); // ✅ Usando setter público
        p.setIdade(30);    // ✅
        
        System.out.println(p.getNome()); // ✅ Lendo com getter
        System.out.println(p.getIdade());
        
        // p.nome = "Maria"; // ❌ ERRO: atributo privado!
    }
}
```

## **Vantagens Dessa Abordagem**

✅ **Validação centralizada**: Todas as regras ficam nos setters  
✅ **Controle de acesso**: Pode ter atributos "somente leitura" (apenas getter)  
✅ **Manutenção**: Se precisar mudar como o atributo é armazenado, não quebra o código externo  

## **Padrão de Nomenclatura**
- **Getters**: `get` + nome do atributo (ex: `getNome()`)
- **Setters**: `set` + nome do atributo (ex: `setNome()`)
- Para booleanos: `is` + nome (ex: `isAtivo()`)

## **Exemplo Avançado com Lógica**
```java
public class ContaBancaria {
    private double saldo;

    public void depositar(double valor) {
        if (valor <= 0) {
            throw new IllegalArgumentException("Valor inválido");
        }
        this.saldo += valor;
    }

    public boolean sacar(double valor) {
        if (valor > 0 && valor <= saldo) {
            this.saldo -= valor;
            return true;
        }
        return false;
    }

    // Getter sem setter (saldo só muda via depositar/sacar)
    public double getSaldo() {
        return this.saldo;
    }
}
```

## **Quando Não Usar Getters/Setters?**
- Para classes **imutáveis** (onde atributos não mudam após criação)
- Em **DTOs muito simples** (alguns frameworks esperam atributos públicos)
- Em **classes internas** de escopo restrito

**Dica para iniciantes:** Comece sempre com atributos `private` e crie getters/setters conforme a necessidade! 😊

Quer ver como isso funciona com herança ou como o IntelliJ pode gerar automaticamente esses métodos? Posso te mostrar!
