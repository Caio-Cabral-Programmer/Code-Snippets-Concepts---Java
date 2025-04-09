### **Tipos Primitivos em Java**  

Em Java, os **tipos primitivos** são dados básicos que **não são objetos** e armazenam valores diretamente na memória. Eles são mais eficientes em termos de desempenho e consumo de memória do que objetos.  

Existem **8 tipos primitivos** em Java, divididos em 4 categorias:  

---

## **1. Tipos Inteiros (números sem casas decimais)**  

| Tipo    | Tamanho (bits) | Faixa de Valores                           | Exemplo          |
|---------|---------------|--------------------------------------------|------------------|
| `byte`  | 8 bits        | -128 a 127                                 | `byte b = 100;`  |
| `short` | 16 bits       | -32.768 a 32.767                           | `short s = 5000;`|
| `int`   | 32 bits       | -2.147.483.648 a 2.147.483.647             | `int i = 200000;`|
| `long`  | 64 bits       | -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807 | `long l = 10000000000L;` |

🔹 **Observações:**  
- O `long` precisa do sufixo **`L`** (ex: `100L`).  
- O `int` é o tipo mais usado para números inteiros.  

---

## **2. Tipos de Ponto Flutuante (números decimais)**  

| Tipo      | Tamanho (bits) | Precisão               | Exemplo            |
|-----------|---------------|------------------------|--------------------|
| `float`  | 32 bits       | ~6-7 dígitos decimais  | `float f = 3.14f;` |
| `double` | 64 bits       | ~15 dígitos decimais   | `double d = 3.1415926535;` |

🔹 **Observações:**  
- O `float` precisa do sufixo **`f`** (ex: `5.75f`).  
- O `double` é mais preciso e é o padrão para decimais em Java.  

---

## **3. Tipo `char` (caractere único)**  

| Tipo   | Tamanho (bits) | Descrição                     | Exemplo          |
|--------|---------------|-------------------------------|------------------|
| `char` | 16 bits       | Armazena **um único caractere** Unicode | `char c = 'A';` |

🔹 **Observações:**  
- Usa **aspas simples** (`' '`).  
- Pode armazenar letras, números, símbolos e até caracteres Unicode (`'\u0041'` = 'A').  

---

## **4. Tipo `boolean` (verdadeiro/falso)**  

| Tipo       | Tamanho (não especificado) | Valores Possíveis | Exemplo           |
|------------|---------------------------|-------------------|-------------------|
| `boolean` | ~1 bit (otimizado)        | `true` ou `false` | `boolean ligado = true;` |

🔹 **Observações:**  
- Usado em condições (`if`, `while`, etc.).  
- Não é convertido para `0` ou `1` como em algumas linguagens.  

---

## **Exemplo Completo com Todos os Tipos Primitivos**  

```java
public class TiposPrimitivos {
    public static void main(String[] args) {
        // Inteiros
        byte b = 120;
        short s = 32000;
        int i = 2_000_000;  // O "_" melhora a legibilidade
        long l = 9_000_000_000L;

        // Decimais
        float f = 3.14f;
        double d = 3.1415926535;

        // Caractere
        char letra = 'J';
        char simbolo = '\u00A9'; // © (símbolo de copyright)

        // Booleano
        boolean javaEhLegal = true;

        System.out.println("byte: " + b);
        System.out.println("double: " + d);
        System.out.println("char: " + letra + " " + simbolo);
    }
}
```

---

## **Quando Usar Cada Tipo?**  

| Tipo       | Quando Usar?                                                                 |
|------------|-----------------------------------------------------------------------------|
| `int`      | Números inteiros em geral (idade, contador, etc.).                          |
| `long`     | Números muito grandes (ex: população mundial).                              |
| `double`   | Decimais de alta precisão (ex: cálculos científicos, financeiros).          |
| `float`    | Decimais quando economia de memória é crítica (raro em aplicações modernas).|
| `char`     | Armazenar um único caractere (ex: letras, símbolos).                        |
| `boolean`  | Condições lógicas (ex: `if (estaChovendo) { ... }`).                        |
| `byte`/`short` | Quando economia de memória é essencial (ex: processamento de arquivos binários). |

---

## **Valores Padrão (Quando Não Inicializadas)**  

Se uma variável primitiva for declarada como **atributo de classe**, ela recebe um valor padrão:  

| Tipo       | Valor Padrão  |
|------------|--------------|
| `byte`     | `0`          |
| `short`    | `0`          |
| `int`      | `0`          |
| `long`     | `0L`         |
| `float`    | `0.0f`       |
| `double`   | `0.0d`       |
| `char`     | `'\u0000'` (caractere nulo) |
| `boolean`  | `false`      |

⚠️ **Cuidado!** Variáveis locais **não têm valor padrão** e devem ser inicializadas manualmente.  

---

### **Resumo Final**  
✅ Java tem **8 tipos primitivos**:  
- **4 inteiros**: `byte`, `short`, `int`, `long`  
- **2 decimais**: `float`, `double`  
- **1 caractere**: `char`  
- **1 booleano**: `boolean`  

Se tiver dúvidas sobre algum tipo específico, pode perguntar! 😊