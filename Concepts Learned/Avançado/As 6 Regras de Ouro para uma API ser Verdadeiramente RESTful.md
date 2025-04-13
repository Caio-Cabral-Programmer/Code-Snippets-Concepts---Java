# 📜 As 6 Regras de Ouro para uma API ser Verdadeiramente RESTful

Vou te explicar como se fosse uma receita de bolo para criar a API perfeita! 🎂

## 1. **Interface Uniforme (Uniform Interface)** - 🧩
**"Todos falam a mesma língua"**

- **Recursos identificáveis**: Cada coisa é um endereço único (URI)
  - `/clientes/123` (Certo)
  - `/buscar_cliente?id=123` (Errado - não é uniforme)

- **Representações padronizadas**: Usar formatos como JSON/XML
  ```json
  {
    "id": 123,
    "nome": "João",
    "email": "joao@exemplo.com"
  }
  ```

- **Hipermídia (HATEOAS)**: Links para navegar na API
  ```json
  {
    "id": 123,
    "links": [
      { "rel": "self", "href": "/clientes/123" },
      { "rel": "pedidos", "href": "/clientes/123/pedidos" }
    ]
  }
  ```

## 2. **Cliente-Servidor Sem Estado (Stateless)** - 🧑💻➡️🖥️
**"Cada pedido é independente"**

- O servidor **não guarda** informações do cliente entre requisições
- Cada request deve ter **TODA** informação necessária
  - **Certo**: Token JWT no header
  - **Errado**: Usar sessão no servidor

## 3. **Cacheável** - 📦
**"Guardar cópias para agilizar"**

- Respostas devem dizer se podem ser cacheadas
  ```http
  HTTP/1.1 200 OK
  Cache-Control: max-age=3600
  ```

- Exemplos de cache:
  - `Cache-Control: no-store` (Nunca cachear)
  - `Cache-Control: public, max-age=86400` (Cachear por 1 dia)

## 4. **Sistema em Camadas (Layered System)** - 🥞
**"Dividir o trabalho"**

- Pode ter intermediários:
  - Load balancers: `Cliente → Balanceador → Servidor`
  - Proxies: `Cliente → Proxy Cache → API`
  - Gateways: `Cliente → Gateway → Microsserviços`

- O cliente **não sabe** quantas camadas existem

## 5. **Código Sob Demanda (Code-On-Demand - Opcional)** - ⏬
**"Baixar apps extras quando precisar"**

- O servidor pode enviar código executável (como JavaScript)
  ```json
  {
    "dados": [1, 2, 3],
    "script": "function soma() { return this.dados.reduce((a,b) => a+b); }"
  }
  ```

## 6. **Manipulação de Recursos por Representação** - ✨
**"Só mexer através das representações"**

- Nunca alterar o recurso diretamente, sempre enviar a representação completa
  - **PUT**: Enviar objeto completo para atualização
  - **PATCH**: Enviar só campos alterados (mas ainda é uma representação)

## 🏆 Teste: Sua API é RESTful de Verdade?

| Regra                | Exemplo Cumprindo                          | Exemplo Violando                          |
|----------------------|-------------------------------------------|-------------------------------------------|
| Interface Uniforme   | GET /livros/1 (sem verbo na URL)          | GET /buscarLivro?id=1                     |
| Stateless            | Token JWT em cada requisição              | Sessão guardada no servidor               |
| Cacheável            | Headers Cache-Control definidos           | Sem controle de cache                     |
| Sistema em Camadas   | Usando API Gateway                        | Cliente acessa DB diretamente             |
| Code-On-Demand       | Enviando JavaScript para validação        | Nunca envia código                        |
| Manipulação por Representação | PUT /clientes/1 com JSON completo    | SQL injection direto no endpoint          |

## 🔥 Exemplo Prático (Spring Boot RESTful)

```java
@RestController
@RequestMapping("/api/v1/livros")
public class LivroController {

    @GetMapping(produces = MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<Resource<Livro>> listarTodos() {
        List<Livro> livros = livroService.findAll();
        
        // HATEOAS - Hipermídia
        Link selfLink = linkTo(methodOn(LivroController.class).listarTodos()).withSelfRel();
        
        Resource<Livro> resource = new Resource<>(livros);
        resource.add(selfLink);
        
        // Cache
        return ResponseEntity.ok()
               .cacheControl(CacheControl.maxAge(1, TimeUnit.HOURS))
               .body(resource);
    }

    @PostMapping(consumes = MediaType.APPLICATION_JSON_VALUE)
    public ResponseEntity<Void> criar(@Valid @RequestBody Livro livro, 
                                    UriComponentsBuilder uriBuilder) {
        Livro saved = livroService.save(livro);
        
        // Interface Uniforme - URI para o novo recurso
        URI location = uriBuilder.path("/api/v1/livros/{id}")
                               .buildAndExpand(saved.getId())
                               .toUri();
        
        return ResponseEntity.created(location).build();
    }
}
```

## 📚 Evolução Histórica

1. **Arcaico (RPC-style)**:
   - `/getUser`
   - `/updateOrder`
   - Cada ação é um endpoint diferente

2. **REST Básico**:
   - Usa recursos (`/users`, `/orders`)
   - Mas sem HATEOAS, cache, etc.

3. **RESTful Completo**:
   - Cumpre todas as 6 regras
   - Padronização total

Dica: Comece implementando as regras 1 e 2 (Uniform Interface e Stateless), depois vá evoluindo para as demais! 🚀