# Spring MVC: Guia Detalhado para Iniciantes em Java

## O que é Spring MVC?

Spring MVC é um **framework para desenvolvimento web** dentro do ecossistema Spring que segue o padrão **Model-View-Controller** (MVC). Ele simplifica a criação de aplicações web Java, fornecendo uma estrutura organizada e muitas funcionalidades prontas para uso.

## Analogia para Entender o Spring MVC

Imagine um restaurante:
- **Cliente**: Faz um pedido (requisição HTTP)
- **Garçom (Controller)**: Recebe o pedido e coordena tudo
- **Cozinha (Model)**: Prepara os dados/negócio
- **Garçom**: Leva a comida pronta (View) para o cliente

## Componentes Principais do Spring MVC

### 1. DispatcherServlet (O "Cérebro")
- É a porta de entrada de todas as requisições
- Coordena todo o fluxo da aplicação
- **Como funciona**:
  ```mermaid
  sequenceDiagram
    Cliente->>+DispatcherServlet: Requisição HTTP
    DispatcherServlet->>+Controller: Encaminha requisição
    Controller->>+Model: Processa dados
    Model-->>-Controller: Retorna dados
    Controller-->>-DispatcherServlet: Retorna ModelAndView
    DispatcherServlet->>+View: Renderiza resposta
    View-->>-DispatcherServlet: HTML/JSON
    DispatcherServlet-->>-Cliente: Resposta HTTP
  ```

### 2. Controllers (Os "Garçons")
- Classes que lidam com requisições específicas
- Exemplo básico:
```java
@Controller
public class HomeController {
    
    @GetMapping("/ola")
    public String dizerOla(Model model) {
        model.addAttribute("mensagem", "Olá, Spring MVC!");
        return "saudacao"; // Nome da view (template)
    }
}
```

### 3. Model (A "Cozinha")
- Contém os dados da aplicação e regras de negócio
- Representado por objetos Java simples (POJOs)

### 4. View (O "Prato Final")
- Como os dados são apresentados (HTML, JSON, XML)
- Tecnologias comuns:
  - Thymeleaf (recomendado para iniciantes)
  - JSP
  - FreeMarker

## Fluxo Completo de uma Requisição

1. **Requisição chega** no `DispatcherServlet`
2. **Mapeamento**: Servlet decide qual Controller deve tratar
3. **Controller processa**:
   - Recebe parâmetros
   - Chama serviços (Model)
   - Prepara dados para a View
4. **Resposta é renderizada** pela View
5. **Resposta é enviada** ao cliente

## Configuração Básica (Spring Boot)

Spring Boot simplifica muito a configuração. Veja um exemplo mínimo:

1. **Classe principal**:
```java
@SpringBootApplication
public class MinhaAplicacao {
    public static void main(String[] args) {
        SpringApplication.run(MinhaAplicacao.class, args);
    }
}
```

2. **Controller** (como o exemplo anterior)
3. **View** (em `src/main/resources/templates/saudacao.html`):
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Saudação</title>
</head>
<body>
    <h1 th:text="${mensagem}">Mensagem padrão</h1>
</body>
</html>
```

## Anotações Essenciais do Spring MVC

| Anotação | Exemplo | Para que serve |
|----------|---------|----------------|
| `@Controller` | `@Controller class MeuCtrl` | Define uma classe como Controller |
| `@RequestMapping` | `@RequestMapping("/pessoas")` | Mapeia URLs para métodos |
| `@GetMapping` | `@GetMapping("/listar")` | Mapeia requisições GET |
| `@PostMapping` | `@PostMapping("/salvar")` | Mapeia requisições POST |
| `@RequestParam` | `(@RequestParam String nome)` | Obtém parâmetros da URL |
| `@PathVariable` | `(@PathVariable Long id)` | Obtém valores do caminho da URL |
| `@ModelAttribute` | `(@ModelAttribute Usuario user)` | Vincula parâmetros a um objeto |
| `@ResponseBody` | `@ResponseBody String metodo()` | Indica que o retorno é a resposta direta |

## Exemplo Prático Completo

### 1. Model (Pessoa.java)
```java
public class Pessoa {
    private String nome;
    private int idade;
    // getters e setters
}
```

### 2. Controller (PessoaController.java)
```java
@Controller
@RequestMapping("/pessoas")
public class PessoaController {
    
    @GetMapping("/form")
    public String mostrarForm(Model model) {
        model.addAttribute("pessoa", new Pessoa());
        return "form-pessoa";
    }
    
    @PostMapping("/salvar")
    public String salvarPessoa(@ModelAttribute Pessoa pessoa) {
        System.out.println("Salvando: " + pessoa.getNome());
        return "redirect:/pessoas/listar";
    }
    
    @GetMapping("/listar")
    public String listarPessoas(Model model) {
        // Na prática, viria de um banco de dados
        List<Pessoa> pessoas = Arrays.asList(
            new Pessoa("Ana", 25),
            new Pessoa("João", 30)
        );
        model.addAttribute("pessoas", pessoas);
        return "lista-pessoas";
    }
}
```

### 3. View (form-pessoa.html)
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<body>
    <form th:action="@{/pessoas/salvar}" th:object="${pessoa}" method="post">
        Nome: <input type="text" th:field="*{nome}"><br>
        Idade: <input type="number" th:field="*{idade}"><br>
        <button type="submit">Salvar</button>
    </form>
</body>
</html>
```

### 4. View (lista-pessoas.html)
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<body>
    <h1>Lista de Pessoas</h1>
    <ul>
        <li th:each="pessoa : ${pessoas}">
            <span th:text="${pessoa.nome}">Nome</span> - 
            <span th:text="${pessoa.idade}">Idade</span>
        </li>
    </ul>
    <a href="/pessoas/form">Adicionar nova</a>
</body>
</html>
```

## Vantagens do Spring MVC

1. **Organização clara**: Separação entre lógica, dados e apresentação
2. **Flexibilidade**: Pode trabalhar com diversas tecnologias de view
3. **Produtividade**: Muitas tarefas comuns já estão prontas
4. **Integração**: Funciona bem com outros módulos Spring (Security, Data, etc.)
5. **Comunidade ativa**: Muitos recursos e ajuda disponível

## Dicas para Iniciantes

1. Comece com Spring Boot - ele configura automaticamente o Spring MVC
2. Use Thymeleaf para templates - é mais simples que JSP para começar
3. Entenda bem o fluxo MVC antes de adicionar complexidade
4. Pratique criando:
   - Um sistema de tarefas (TODO list)
   - Um cadastro de produtos
   - Um blog simples
5. Use o `Spring Initializr` (https://start.spring.io) para criar projetos rapidamente

Lembre-se: Spring MVC parece complexo no início, mas depois que você entende o padrão MVC básico, tudo começa a fazer sentido!