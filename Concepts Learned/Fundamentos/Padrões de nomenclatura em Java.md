# **Padrões de Nomenclatura em Java (Convenções de Código)**

Os padrões de nomenclatura em Java seguem as **Java Code Conventions** da Oracle e são amplamente adotados pela comunidade. Eles ajudam a manter o código legível e consistente. Vamos dividir por categorias:

## **1. Classes e Interfaces**
- **PascalCase** (primeira letra de cada palavra em maiúsculo)
- **Nomes substantivos** que representam o propósito da classe
- **Interfaces** frequentemente são adjetivos (terminando com "able" quando aplicável)

```java
// Classes
class Carro {}
class BancoDeDados {}
class CalculadoraCientifica {}

// Interfaces
interface Runnable {}
interface Serializavel {}
interface Comparable {}
```

## **2. Métodos**
- **camelCase** (primeira letra minúscula, demais palavras com inicial maiúscula)
- **Nomes verbais** que descrevem ações
- Nomes comuns: `get`, `set`, `is`, `has`, `calculate`, `find`

```java
void acelerar() {}
String getNome() {}
boolean isAtivo() {}
double calcularImposto() {}
```

## **3. Variáveis e Parâmetros**
- **camelCase** (igual aos métodos)
- Nomes descritivos e curtos (evitar abreviações obscuras)
- Tipos específicos podem ter sufixos (ex: `lista` para coleções)

```java
int idade;
String nomeCompleto;
double saldoEmConta;
List<String> nomesLista;
```

## **4. Constantes**
- **SCREAMING_SNAKE_CASE** (todas letras maiúsculas com underscore)
- Declaradas com `final static`

```java
final static double PI = 3.141592;
final static int MAX_TENTATIVAS = 3;
final static String NOME_APLICACAO = "MeuApp";
```

## **5. Pacotes**
- **Todas letras minúsculas**
- **Estrutura hierárquica** inversa do domínio (ex: `com.empresa.projeto`)
- Evitar palavras únicas genéricas (usar `utils` em vez de `utility`)

```java
package br.com.empresa.financeiro;
package org.openjdk.jdk;
```

## **6. Enums (Tipos Enumeração)**
- **PascalCase** (como classes)
- **Valores enum** em SCREAMING_SNAKE_CASE (como constantes)

```java
enum StatusPedido {
    EM_PROCESSAMENTO,
    ENVIADO,
    ENTREGUE
}
```

## **7. Exceções**
- **PascalCase** (como classes)
- **Sufixo `Exception`** para classes de exceção

```java
class SaldoInsuficienteException extends Exception {}
class FormatoInvalidoException extends RuntimeException {}
```

## **8. Genéricos (Generics)**
- Letras maiúsculas únicas (convenção comum):
  - `T` para Type (tipo genérico)
  - `E` para Element (coleções)
  - `K` para Key (mapas)
  - `V` para Value (mapas)

```java
class Caixa<T> {}
interface List<E> {}
class Mapa<K, V> {}
```

## **9. Convenções Especiais**
### **Métodos Booleanos**
- Prefixos com `is`, `has`, `can`, `should` para clareza:

```java
boolean isVazio() {}
boolean hasNext() {}
boolean canExecute() {}
```

### **Métodos Getter/Setter**
- Padrão JavaBeans:

```java
private String nome;

public String getNome() {
    return nome;
}

public void setNome(String nome) {
    this.nome = nome;
}
```

## **10. Exemplos de Nomes a Evitar**
❌ `int a;` (muito genérico)  
❌ `String STR;` (constante sem `final`)  
❌ `class userManager {}` (deveria ser `UserManager`)  
❌ `void CalculateTotal() {}` (método em PascalCase)  

## **11. Ferramentas para Verificação**
- **Checkstyle**: Plugin para IDEs que valida convenções
- **SonarLint**: Analisa código em tempo real
- **PMD**: Outra ferramenta de análise estática

## **Por que Seguir Padrões?**
✔ **Legibilidade**: Código mais fácil de entender  
✔ **Manutenibilidade**: Facilita a colaboração em equipe  
✔ **Consistência**: Padronização em projetos grandes  
✔ **Evitar erros**: Nomes confusos podem causar bugs  

## **Exemplo Completo**
```java
package com.exemplo.projeto.utils;

public class CalculadoraFinanceira {
    private static final double TAXA_JUROS = 0.05;
    
    private double saldoAtual;
    
    public double calcularJuros(int meses) {
        return saldoAtual * TAXA_JUROS * meses;
    }
    
    public boolean isSaldoPositivo() {
        return saldoAtual > 0;
    }
}
```

Dominar essas convenções é essencial para escrever código Java profissional! Pratique em seus projetos. 😊