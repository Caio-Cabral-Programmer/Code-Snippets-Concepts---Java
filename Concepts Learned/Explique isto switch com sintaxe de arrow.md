A partir do Java 12, foi introduzida uma nova sintaxe para a estrutura `switch` chamada **"switch com sintaxe de arrow"** (ou **"switch expression"**). Essa nova sintaxe torna o `switch` mais conciso, legível e menos propenso a erros, especialmente em comparação com o `switch` tradicional. A principal diferença é o uso do operador `->` (arrow) para separar o caso (case) do bloco de código que deve ser executado.

---

### Sintaxe básica
Aqui está a sintaxe básica do `switch` com arrow:

```java
switch (variável) {
    case valor1 -> // código a ser executado se variável == valor1
    case valor2 -> // código a ser executado se variável == valor2
    default ->    // código a ser executado se nenhum caso for correspondido
}
```

---

### Diferenças em relação ao `switch` tradicional
1. **Uso de `->`**:
   - Substitui os dois-pontos (`:`) do `switch` tradicional.
   - Elimina a necessidade de usar `break` para evitar o "fall-through" (execução de múltiplos casos).

2. **Retorno de valores**:
   - O `switch` com arrow pode retornar valores diretamente, funcionando como uma expressão.

3. **Código mais limpo**:
   - Reduz a verbosidade e evita erros comuns, como esquecer o `break`.

---

### Exemplo comparativo

#### `switch` tradicional:
```java
int dia = 3;
String nomeDia;

switch (dia) {
    case 1:
        nomeDia = "Domingo";
        break;
    case 2:
        nomeDia = "Segunda-feira";
        break;
    case 3:
        nomeDia = "Terça-feira";
        break;
    default:
        nomeDia = "Dia inválido";
}
System.out.println(nomeDia); // Saída: Terça-feira
```

#### `switch` com arrow:
```java
int dia = 3;
String nomeDia = switch (dia) {
    case 1 -> "Domingo";
    case 2 -> "Segunda-feira";
    case 3 -> "Terça-feira";
    default -> "Dia inválido";
};
System.out.println(nomeDia); // Saída: Terça-feira
```

---

### Vantagens do `switch` com arrow
1. **Menos verboso**:
   - Não é necessário usar `break` ou dois-pontos (`:`).

2. **Evita fall-through**:
   - O `switch` com arrow não executa múltiplos casos por padrão, eliminando o risco de esquecer o `break`.

3. **Pode retornar valores**:
   - O `switch` com arrow pode ser usado como uma expressão, retornando um valor diretamente.

4. **Suporte a múltiplos casos**:
   - Você pode agrupar vários casos para executar o mesmo código.

---

### Exemplos avançados

#### 1. Retornando valores
O `switch` com arrow pode retornar valores diretamente, o que é útil em expressões:

```java
int dia = 3;
String nomeDia = switch (dia) {
    case 1 -> "Domingo";
    case 2 -> "Segunda-feira";
    case 3 -> "Terça-feira";
    default -> "Dia inválido";
};
System.out.println(nomeDia); // Saída: Terça-feira
```

#### 2. Agrupando casos
Você pode agrupar vários casos para executar o mesmo código:

```java
int mes = 2;
int diasNoMes = switch (mes) {
    case 1, 3, 5, 7, 8, 10, 12 -> 31;
    case 4, 6, 9, 11 -> 30;
    case 2 -> 28; // Fevereiro (ignorando anos bissextos)
    default -> throw new IllegalArgumentException("Mês inválido: " + mes);
};
System.out.println("Dias no mês: " + diasNoMes); // Saída: Dias no mês: 28
```

#### 3. Blocos de código
Se você precisar executar múltiplas instruções para um caso, pode usar um bloco de código com `{}`:

```java
int dia = 3;
String nomeDia = switch (dia) {
    case 1 -> "Domingo";
    case 2 -> "Segunda-feira";
    case 3 -> {
        System.out.println("É terça-feira!");
        yield "Terça-feira"; // Usado para retornar um valor em blocos
    }
    default -> "Dia inválido";
};
System.out.println(nomeDia); // Saída: É terça-feira! \n Terça-feira
```

---

### Resumo
- O `switch` com arrow (`->`) é uma sintaxe moderna introduzida no Java 12.
- Ele é mais conciso, evita o fall-through e pode retornar valores diretamente.
- É especialmente útil para simplificar o código e evitar erros comuns do `switch` tradicional.

Se precisar de mais exemplos ou explicações, é só perguntar! 😊
