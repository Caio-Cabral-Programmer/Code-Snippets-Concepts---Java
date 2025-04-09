
---

## **Tipos de Relacionamentos em UML e Java**  

Além da **herança**, existem outros relacionamentos entre classes:  

| **Tipo**       | **Descrição**                                                                 | **Exemplo em Java**                          | **Símbolo UML** |
|----------------|-------------------------------------------------------------------------------|---------------------------------------------|----------------|
| **Herança**    | Uma classe **estende** outra (`extends`).                                     | `class Carro extends Veiculo`               | ◁─── (seta vazia) |
| **Associação** | Relação fraca onde objetos **usam** outros, mas não dependem para existir.    | `Professor` ensina `Aluno` (ambos independentes) | ───── (linha simples) |
| **Agregação**  | Relação "tem um" onde um objeto **contém** outro, mas podem existir separados. | `Departamento` tem `Professores` (mas professores existem sem departamento) | ◇─── (losango vazio) |
| **Composição** | Relação forte onde um objeto **é parte** de outro e não existe separadamente. | `Casa` tem `Quartos` (quartos não existem sem a casa) | ◆─── (losango preenchido) |

---

### **Exemplo Detalhado dos Relacionamentos**

#### **1. Herança (Generalização)**
```java
class Animal {
    void comer() {
        System.out.println("Comendo...");
    }
}

class Cachorro extends Animal {  // Cachorro É UM Animal
    void latir() {
        System.out.println("Au au!");
    }
}
```
**UML:**  
```
       Animal
         △
         |
     Cachorro
```

---

#### **2. Associação (Objetos se relacionam, mas são independentes)**
```java
class Professor {
    String nome;
}

class Aluno {
    String nome;
    void estudarCom(Professor prof) {  // Aluno associa-se com Professor
        System.out.println(nome + " estuda com " + prof.nome);
    }
}
```
**UML:**  
```
Professor ───── Aluno
```

---

#### **3. Agregação (Tem um, mas pode existir separadamente)**
```java
class Departamento {
    List<Professor> professores;  // Departamento TEM Professores (mas eles existem sem o departamento)
}
```
**UML:**  
```
Departamento ◇─── Professor
```

---

#### **4. Composição (Parte de, não existe separadamente)**
```java
class Casa {
    List<Quarto> quartos;  // Casa TEM Quartos (e quartos não existem sem a casa)
    Casa() {
        quartos = new ArrayList<>();
        quartos.add(new Quarto());  // Quarto é criado dentro da Casa
    }
}

class Quarto { }
```
**UML:**  
```
Casa ◆─── Quarto
```

---

## **3. Quando Usar Cada Relacionamento?**  

| **Relacionamento** | **Quando Usar?**                                                                 |
|--------------------|---------------------------------------------------------------------------------|
| **Herança**        | Quando uma classe **é uma versão mais especializada** de outra (ex: `Cachorro` é um `Animal`). |
| **Associação**     | Quando um objeto **usa outro**, mas não depende dele para existir (ex: `Aluno` e `Professor`). |
| **Agregação**      | Quando um objeto **contém outro**, mas ele pode existir separadamente (ex: `Departamento` e `Professor`). |
| **Composição**     | Quando um objeto **é parte essencial** de outro (ex: `Casa` e `Quarto`). |

---

## **4. Resumo Final**  

✅ **Herança (`extends`)** → "É um" (ex: `Carro` é um `Veículo`)  
✅ **Associação** → "Usa" (ex: `Aluno` estuda com `Professor`)  
✅ **Agregação (`List<>`)** → "Tem um" (relação fraca, objetos independentes)  
✅ **Composição (`new` dentro da classe)** → "Tem um" (relação forte, objeto dependente)  

# **Dependência em Java e UML - Explicação para Iniciantes**  

A **dependência** é um tipo de relacionamento em que uma classe **usa** outra temporariamente, sem manter uma referência duradoura. É o mais fraco dos relacionamentos em UML e ocorre quando uma classe:  
✔ **Recebe um objeto como parâmetro**  
✔ **Retorna um objeto como resultado**  
✔ **Usa um objeto dentro de um método**  

---

## **1. Como Identificar uma Dependência?**  
Se `ClasseA` depende de `ClasseB`, significa que:  
➡ `ClasseA` **não armazena** `ClasseB` como atributo.  
➡ `ClasseA` **precisa** de `ClasseB` apenas para executar uma operação específica.  

---

## **2. Exemplo em Java**  

### **Cenário:**  
- `Escola` depende de `Professor` para `realizarAula()`, mas não guarda o professor como atributo.  

```java
class Professor {
    void ensinar() {
        System.out.println("Ensinando...");
    }
}

class Escola {
    // Dependência: Escola usa Professor temporariamente
    void realizarAula(Professor prof) {  // Recebe Professor como parâmetro
        prof.ensinar();
    }
}

public class Main {
    public static void main(String[] args) {
        Escola minhaEscola = new Escola();
        Professor prof = new Professor();
        
        minhaEscola.realizarAula(prof);  // Escola depende de Professor aqui
    }
}
```
**Saída:**  
```
Ensinando...
```

---

## **3. Representação em UML**  
A dependência é representada por uma **seta tracejada** (`----->`).  

```
Escola ------> Professor
```

---

## **4. Diferença Entre Dependência e Associação/Agregação**  

| **Tipo**         | **Duração**          | **Exemplo**                                  | **UML**       |
|------------------|----------------------|---------------------------------------------|---------------|
| **Dependência**  | Temporária (método)  | `Escola` usa `Professor` só em `realizarAula()` | `----->`      |
| **Associação**   | Permanente (atributo)| `Escola` tem `Professor` como atributo       | `-----`       |
| **Agregação**    | Permanente, mas fraca| `Departamento` tem `Professores` (opcional)  | `◇----`       |

---

## **5. Quando Usar Dependência?**  
Use quando:  
🔹 Uma classe **precisa de outra apenas para uma operação específica**.  
🔹 Não faz sentido manter uma **referência duradoura**.  

Exemplos comuns:  
✔ Passar um `Scanner` como parâmetro para ler dados.  
✔ Usar um `Calendar` para formatar uma data dentro de um método.  

---

## **6. Exercício Prático**  
Crie uma classe `Calculadora` que depende de `Logger` para registrar operações:  

```java
class Logger {
    void log(String mensagem) {
        System.out.println("[LOG] " + mensagem);
    }
}

class Calculadora {
    // Dependência: Calculadora usa Logger temporariamente
    void somar(int a, int b, Logger logger) {
        int resultado = a + b;
        logger.log("Soma: " + resultado);
    }
}

public class Main {
    public static void main(String[] args) {
        Calculadora calc = new Calculadora();
        Logger log = new Logger();
        
        calc.somar(5, 3, log);  // Dependência aqui
    }
}
```
**Saída:**  
```
[LOG] Soma: 8
```

---

## **7. Resumo**  
✅ **Dependência** = Uso temporário (parâmetro, retorno, método).  
✅ **Mais fraca** que associação/agregação/composição.  
✅ **Símbolo UML**: `----->` (seta tracejada).  

É um conceito importante para **evitar acoplamento desnecessário** entre classes! 🚀