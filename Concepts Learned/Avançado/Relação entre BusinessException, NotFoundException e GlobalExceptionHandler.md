


# Entendendo as Exceções em Java Spring: BusinessException, NotFoundException e GlobalExceptionHandler

Olá pequeno(a) programador(a)! Hoje vamos entender como funciona o sistema de "avisos de problemas" em nossa aplicação Java. Vamos imaginar que estamos construindo um parque de diversões, e precisamos de um sistema para lidar com diferentes tipos de problemas que podem acontecer.

## 1. O que são Exceções em Java?

Antes de tudo, vamos entender o que são exceções. Exceções são como "alarmes" que tocam quando algo dá errado no nosso código. Em vez de deixar o programa quebrar completamente, Java nos permite "capturar" esses alarmes e decidir o que fazer quando eles tocam.

## 2. A Classe BusinessException

Vamos olhar para o código da `BusinessException`:

```java
package me.dio.exception;

public class BusinessException extends RuntimeException {

    private static final long serialVersionUID = 1L;

    public BusinessException(String message) {
        super(message);
    }
}
```

Esta classe é como um tipo especial de alarme que toca quando há um problema com as regras de negócio da nossa aplicação.

### Explicando cada parte:

- `public class BusinessException extends RuntimeException`: Estamos criando um novo tipo de alarme chamado `BusinessException` que é baseado em um alarme mais geral chamado `RuntimeException`.

- `private static final long serialVersionUID = 1L;`: Este é um número especial que ajuda Java a identificar nossa classe quando estamos enviando objetos pela rede ou salvando em arquivos. É como o número de série de um brinquedo.

- `public BusinessException(String message) { super(message); }`: Este é o construtor da nossa classe. Quando criamos um novo alarme `BusinessException`, podemos passar uma mensagem explicando o que deu errado. O `super(message)` envia essa mensagem para o alarme pai (`RuntimeException`).

## 3. A Classe NotFoundException

Agora, vamos olhar para a classe `NotFoundException`:

```java
package me.dio.exception;

public class NotFoundException extends BusinessException {

    private static final long serialVersionUID = 1L;

    public NotFoundException() {
        super("Resource not found.");
    }
}
```

Esta classe é um tipo ainda mais específico de alarme que toca quando não conseguimos encontrar algo que estávamos procurando.

### Explicando cada parte:

- `public class NotFoundException extends BusinessException`: Estamos criando um novo tipo de alarme chamado `NotFoundException` que é baseado no nosso alarme `BusinessException`. Isso significa que `NotFoundException` é um tipo especial de `BusinessException`.

- `private static final long serialVersionUID = 1L;`: Novamente, este é o número de série da nossa classe.

- `public NotFoundException() { super("Resource not found."); }`: Este é o construtor da nossa classe. Diferente da `BusinessException`, não precisamos passar uma mensagem quando criamos um alarme `NotFoundException` - ele sempre usa a mensagem "Resource not found." (Recurso não encontrado).

## 4. A Relação entre BusinessException e NotFoundException

A relação entre `BusinessException` e `NotFoundException` é como a relação entre "problema no parque de diversões" e "brinquedo fechado para manutenção":

- `BusinessException` é um alarme geral para qualquer problema relacionado às regras de negócio da nossa aplicação. É como dizer "Temos um problema no parque de diversões".

- `NotFoundException` é um tipo específico de `BusinessException` que ocorre quando não encontramos algo. É como dizer "Temos um problema no parque de diversões: o brinquedo que você quer está fechado para manutenção".

Como `NotFoundException` estende `BusinessException`, todo `NotFoundException` é também um `BusinessException`, mas nem todo `BusinessException` é um `NotFoundException`.

## 5. O GlobalExceptionHandler

Agora, vamos entender como o `GlobalExceptionHandler` se relaciona com essas exceções:

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    private static final Logger LOGGER = LoggerFactory.getLogger(GlobalExceptionHandler.class);

    @ExceptionHandler(BusinessException.class)
    public ResponseEntity<String> handleBusinessException(BusinessException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.UNPROCESSABLE_ENTITY);
    }

    @ExceptionHandler(NotFoundException.class)
    public ResponseEntity<String> handleNoContentException() {
        return new ResponseEntity<>("Resource ID not found.", HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(Throwable.class)
    public ResponseEntity<String> handleUnexpectedException(Throwable unexpectedException) {
        String message = "Unexpected server error.";
        LOGGER.error(message, unexpectedException);
        return new ResponseEntity<>(message, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

O `GlobalExceptionHandler` é como a central de segurança do nosso parque de diversões. Quando um alarme toca em qualquer lugar do parque, a central de segurança recebe o alerta e decide o que fazer.

### Como funciona:

1. `@RestControllerAdvice`: Esta anotação diz ao Spring que esta classe é responsável por lidar com exceções em toda a aplicação.

2. Para cada tipo de alarme, temos um método específico:

   - `handleBusinessException`: Lida com alarmes do tipo `BusinessException`. Quando um desses alarmes toca, respondemos com a mensagem do alarme e um código de status HTTP 422 (UNPROCESSABLE_ENTITY), que significa "Entendi o que você pediu, mas não posso fazer isso porque tem algo errado com os dados".

   - `handleNoContentException`: Lida com alarmes do tipo `NotFoundException`. Quando um desses alarmes toca, respondemos com a mensagem "Resource ID not found." e um código de status HTTP 404 (NOT_FOUND), que é o famoso erro que você vê quando uma página da web não existe.

   - `handleUnexpectedException`: Lida com qualquer outro tipo de alarme que não seja um dos acima. Quando um desses alarmes toca, registramos o erro no log (para podermos investigar depois) e respondemos com uma mensagem genérica "Unexpected server error." e um código de status HTTP 500 (INTERNAL_SERVER_ERROR), que significa "Algo deu errado no servidor".

## 6. Como Tudo Isso Funciona Junto no Projeto

Vamos ver como essas peças se encaixam no nosso parque de diversões (projeto):

1. **Quando um problema acontece**: Digamos que um usuário tenta acessar um recurso que não existe (como um usuário com ID 999 que não está no banco de dados).

2. **O serviço lança uma exceção**: O serviço (como `UserServiceImpl`) percebe que o recurso não existe e lança um alarme `NotFoundException`:

   ```java
   public User findById(Long id) {
       return this.userRepository.findById(id).orElseThrow(NotFoundException::new);
   }
   ```

3. **O GlobalExceptionHandler captura a exceção**: Como temos um `@ExceptionHandler(NotFoundException.class)` no nosso `GlobalExceptionHandler`, esse método captura o alarme.

4. **Uma resposta apropriada é enviada**: O método `handleNoContentException` cria uma resposta com a mensagem "Resource ID not found." e o código de status HTTP 404.

5. **O cliente recebe a resposta**: Quem estava usando nossa API recebe uma resposta clara indicando que o recurso não foi encontrado.

## 7. Por que Esta Abordagem é Tão Boa?

Esta abordagem de tratamento de exceções tem várias vantagens:

1. **Centralização**: Todo o tratamento de erros está em um único lugar (`GlobalExceptionHandler`), o que torna o código mais organizado.

2. **Hierarquia de exceções**: Ao criar uma hierarquia (`NotFoundException` estende `BusinessException`), podemos tratar exceções de forma mais granular.

3. **Respostas consistentes**: Todos os erros são respondidos de forma padronizada, o que torna nossa API mais previsível e fácil de usar.

4. **Segurança**: Não vazamos detalhes técnicos dos erros para os usuários, apenas mensagens amigáveis.

5. **Facilidade de manutenção**: Se precisarmos mudar como lidamos com um tipo específico de erro, só precisamos alterar um lugar.

## 8. Exemplo Prático

Vamos ver um exemplo prático de como isso funciona:

1. Um usuário tenta atualizar um usuário que não existe:

   ```
   PUT /users/999
   {
     "name": "Novo Nome"
   }
   ```

2. O controlador chama o serviço:

   ```java
   @PutMapping("/{id}")
   public ResponseEntity<UserDto> update(@PathVariable Long id, @RequestBody UserDto userDto) {
       var user = userService.update(id, userDto.toModel());
       return ResponseEntity.ok(new UserDto(user));
   }
   ```

3. O serviço tenta encontrar o usuário, mas ele não existe:

   ```java
   public User update(Long id, User userToUpdate) {
       User dbUser = this.findById(id); // Aqui, findById lança NotFoundException se o usuário não existir
       // resto do código...
   }
   ```

4. O `findById` lança um `NotFoundException`:

   ```java
   public User findById(Long id) {
       return this.userRepository.findById(id).orElseThrow(NotFoundException::new);
   }
   ```

5. O `GlobalExceptionHandler` captura a exceção e cria uma resposta:

   ```java
   @ExceptionHandler(NotFoundException.class)
   public ResponseEntity<String> handleNoContentException() {
       return new ResponseEntity<>("Resource ID not found.", HttpStatus.NOT_FOUND);
   }
   ```

6. O usuário recebe uma resposta com status 404 e a mensagem "Resource ID not found."

## Conclusão

As classes `BusinessException`, `NotFoundException` e `GlobalExceptionHandler` formam um sistema completo e elegante para lidar com problemas em nossa aplicação:

- `BusinessException` é nossa classe base para problemas de negócio
- `NotFoundException` é um tipo específico de problema de negócio (quando algo não é encontrado)
- `GlobalExceptionHandler` é nossa central que captura todos esses problemas e responde de forma apropriada

Este sistema garante que, mesmo quando algo dá errado, nossa aplicação responde de forma educada, clara e útil para os usuários, enquanto nos dá as informações que precisamos para resolver os problemas.

É como ter uma equipe de segurança bem treinada no nosso parque de diversões, garantindo que todos os visitantes tenham uma experiência agradável, mesmo quando um brinquedo está fechado para manutenção! 🎢🎡🎪
