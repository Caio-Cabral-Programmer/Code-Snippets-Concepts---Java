# Como o Java Lida com Múltiplas Classes no Mesmo Arquivo

Em Java, a organização de classes em arquivos segue regras específicas que são importantes para entender como a linguagem estrutura seu código. Vamos explorar isso detalhadamente:

## Regra Básica: Um Arquivo, Uma Classe Pública

**Princípio fundamental**: 
- Cada arquivo `.java` pode conter apenas **uma classe pública**
- O nome do arquivo **deve** corresponder exatamente ao nome da classe pública

**Exemplo correto**:
```java
// Arquivo: MinhaClasse.java
public class MinhaClasse {
    // conteúdo da classe
}
```

## Classes Não-Públicas no Mesmo Arquivo

Um arquivo pode conter múltiplas classes, mas com restrições:
1. Apenas uma classe pode ser `public`
2. As demais classes devem ter visibilidade de pacote (sem modificador `public`)
3. Essas classes secundárias só são visíveis dentro do mesmo pacote

**Exemplo válido**:
```java
// Arquivo: Principal.java
public class Principal {
    public static void main(String[] args) {
        Auxiliar aux = new Auxiliar();
        aux.mensagem();
    }
}

class Auxiliar {
    void mensagem() {
        System.out.println("Classe auxiliar");
    }
}
```

## Classes Internas (Inner Classes)

Java permite definir classes dentro de outras classes, o que é diferente de múltiplas classes no mesmo arquivo:

**Tipos de classes internas**:
1. **Classe interna de instância** (non-static)
2. **Classe interna estática** (static)
3. **Classe local** (dentro de um método)
4. **Classe anônima** (sem nome, para implementações rápidas)

**Exemplo de classe interna**:
```java
public class Externa {
    private int valor = 10;
    
    class Interna {
        void mostrar() {
            System.out.println("Valor: " + valor); // Acessa membros da Externa
        }
    }
}
```

## Compilação e Arquivos .class

Quando você compila um arquivo `.java` com múltiplas classes:
- O compilador gera um arquivo `.class` separado para cada classe
- Para o exemplo anterior (Principal.java), seriam gerados:
  - `Principal.class`
  - `Auxiliar.class`

## Limitações e Boas Práticas

**Problemas com múltiplas classes por arquivo**:
1. Dificuldade de manutenção (código menos organizado)
2. Classes auxiliares não são facilmente reutilizáveis
3. Pode causar confusão em projetos grandes

**Recomendações**:
- Prefira um arquivo por classe (mesmo para classes não-públicas)
- Use classes internas apenas quando fizer sentido lógico (forte acoplamento)
- Para classes utilitárias pequenas, considere usar métodos estáticos

## Casos Especiais

1. **Classes em métodos**:
```java
public class Exemplo {
    public void metodo() {
        class Local {
            void acao() { System.out.println("Ação local"); }
        }
        Local l = new Local();
        l.acao();
    }
}
```

2. **Classes anônimas** (úteis para listeners/interfaces):
```java
button.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        System.out.println("Botão clicado!");
    }
});
```

## Resumo de Regras

| Situação | Permitido? | Nome do Arquivo | Classes Geradas |
|----------|------------|-----------------|-----------------|
| 1 classe pública | Sim | Mesmo nome da classe | 1 .class |
| Múltiplas classes (1 pública) | Sim | Nome da classe pública | 1 .class por classe |
| Múltiplas classes públicas | Não | - | Erro de compilação |
| Classes internas | Sim | Nome da classe externa | Externa.class e Externa$Interna.class |

Lembre-se: enquanto Java permite múltiplas classes por arquivo, adotar a convenção "um arquivo, uma classe" (exceto para classes internas) tornará seu código mais organizado e profissional.