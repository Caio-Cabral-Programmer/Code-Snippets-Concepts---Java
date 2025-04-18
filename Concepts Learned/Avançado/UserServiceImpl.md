
# Explicação sobre a Implementação de Serviço em Java Spring

Olá pequeno(a) programador(a)! Vamos explorar este código como se estivéssemos descobrindo um castelo mágico, sala por sala. Este é um arquivo muito importante chamado `UserServiceImpl.java` que contém regras sobre como gerenciar usuários em um sistema.

## O que é este arquivo?

Este arquivo é como um gerente de uma loja de brinquedos. Ele sabe como:
- Mostrar todos os brinquedos (usuários)
- Encontrar um brinquedo específico
- Adicionar novos brinquedos à loja
- Atualizar informações de um brinquedo
- Remover brinquedos da loja

Mas ele faz isso seguindo regras muito importantes para que tudo funcione direitinho!

## Vamos começar pelo começo

```java
package me.dio.service;

import me.dio.model.User;
import me.dio.repository.UserRepository;
import me.dio.exception.BusinessException;
import me.dio.exception.NotFoundException;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

import static java.util.Optional.ofNullable;
```

Esta parte é como a lista de ingredientes de uma receita. Estamos dizendo ao Java quais "ferramentas" vamos precisar usar:
- `User`: É o nosso brinquedo (o modelo de usuário)
- `UserRepository`: É como a prateleira onde guardamos os brinquedos
- `BusinessException` e `NotFoundException`: São como alarmes que tocam quando algo dá errado
- `@Service` e `@Transactional`: São etiquetas mágicas que dão superpoderes ao nosso código

## A classe e suas características

```java
@Service
public class UserServiceImpl implements UserService {

    /**
     * ID de usuário utilizado na Santander Dev Week 2023.
     * Por isso, vamos criar algumas regras para mantê-lo integro.
     */
    private static final Long UNCHANGEABLE_USER_ID = 1L;

    private final UserRepository userRepository;

    public UserServiceImpl(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
```

Aqui estamos criando nossa classe gerente:
- `@Service`: Esta etiqueta mágica diz ao Spring: "Ei, esta classe é um serviço importante!"
- `implements UserService`: Significa que esta classe promete cumprir todas as tarefas que um `UserService` deve fazer
- `UNCHANGEABLE_USER_ID = 1L`: É um usuário especial (com ID 1) que não pode ser alterado ou removido. É como um brinquedo de exposição que não está à venda!
- O construtor recebe um `UserRepository` que é como nossa prateleira mágica que sabe guardar e encontrar usuários

## Encontrando usuários

```java
@Transactional(readOnly = true)
public List<User> findAll() {
    return this.userRepository.findAll();
}

@Transactional(readOnly = true)
public User findById(Long id) {
    return this.userRepository.findById(id).orElseThrow(NotFoundException::new);
}
```

Estes dois métodos são como "buscadores de brinquedos":
- `findAll()`: Pega TODOS os usuários da prateleira e os coloca em uma lista
- `findById(Long id)`: Procura um usuário específico pelo seu número de identificação
  - Se encontrar, devolve o usuário
  - Se não encontrar, lança um alarme `NotFoundException` (como dizer "Brinquedo não encontrado!")
- `@Transactional(readOnly = true)`: Esta etiqueta diz "Estamos só olhando, não vamos mexer em nada"

## Criando um novo usuário

```java
@Transactional
public User create(User userToCreate) {
    ofNullable(userToCreate).orElseThrow(() -> new BusinessException("User to create must not be null."));
    ofNullable(userToCreate.getAccount()).orElseThrow(() -> new BusinessException("User account must not be null."));
    ofNullable(userToCreate.getCard()).orElseThrow(() -> new BusinessException("User card must not be null."));

    this.validateChangeableId(userToCreate.getId(), "created");
    if (userRepository.existsByAccountNumber(userToCreate.getAccount().getNumber())) {
        throw new BusinessException("This account number already exists.");
    }
    if (userRepository.existsByCardNumber(userToCreate.getCard().getNumber())) {
        throw new BusinessException("This card number already exists.");
    }
    return this.userRepository.save(userToCreate);
}
```

Este método é como um "inspetor de brinquedos novos". Antes de colocar um brinquedo na prateleira, ele faz várias verificações:

1. Verifica se o usuário não é nulo (existe)
2. Verifica se o usuário tem uma conta bancária
3. Verifica se o usuário tem um cartão
4. Verifica se não estamos tentando criar o usuário especial (ID 1)
5. Verifica se o número da conta não existe já (não pode ter duas contas com o mesmo número!)
6. Verifica se o número do cartão não existe já (não pode ter dois cartões com o mesmo número!)

Se passar por todas essas verificações, o usuário é salvo na prateleira (banco de dados).

## Atualizando um usuário

```java
@Transactional
public User update(Long id, User userToUpdate) {
    this.validateChangeableId(id, "updated");
    User dbUser = this.findById(id);
    if (!dbUser.getId().equals(userToUpdate.getId())) {
        throw new BusinessException("Update IDs must be the same.");
    }

    dbUser.setName(userToUpdate.getName());
    dbUser.setAccount(userToUpdate.getAccount());
    dbUser.setCard(userToUpdate.getCard());
    dbUser.setFeatures(userToUpdate.getFeatures());
    dbUser.setNews(userToUpdate.getNews());

    return this.userRepository.save(dbUser);
}
```

Este método é como "reformar um brinquedo". Ele:

1. Verifica se não estamos tentando atualizar o usuário especial (ID 1)
2. Busca o usuário atual no banco de dados
3. Verifica se o ID do usuário encontrado é o mesmo do usuário que queremos atualizar
4. Atualiza todas as informações: nome, conta, cartão, recursos e notícias
5. Salva o usuário atualizado de volta na prateleira

## Removendo um usuário

```java
@Transactional
public void delete(Long id) {
    this.validateChangeableId(id, "deleted");
    User dbUser = this.findById(id);
    this.userRepository.delete(dbUser);
}
```

Este método é como "remover um brinquedo da loja":

1. Verifica se não estamos tentando remover o usuário especial (ID 1)
2. Busca o usuário no banco de dados (para ter certeza que ele existe)
3. Remove o usuário da prateleira

## O método de validação especial

```java
private void validateChangeableId(Long id, String operation) {
    if (UNCHANGEABLE_USER_ID.equals(id)) {
        throw new BusinessException("User with ID %d can not be %s.".formatted(UNCHANGEABLE_USER_ID, operation));
    }
}
```

Este é um método auxiliar que protege o usuário especial (ID 1). Ele verifica se o ID que estamos tentando modificar é o ID 1, e se for, lança um alarme dizendo que este usuário não pode ser modificado.

É como um guarda que protege o brinquedo de exposição da loja!

## Entendendo as anotações especiais

- `@Service`: Diz ao Spring que esta classe é um serviço que contém lógica de negócios
- `@Transactional`: Garante que todas as operações dentro do método sejam tratadas como uma única transação:
  - Se tudo der certo, todas as mudanças são salvas
  - Se algo der errado, todas as mudanças são desfeitas (como se nunca tivessem acontecido)
  - `readOnly = true`: Diz que este método só vai ler dados, não vai modificar nada

## Conclusão

Este arquivo `UserServiceImpl.java` é como um gerente muito cuidadoso de uma loja de brinquedos (usuários). Ele sabe como:

1. Mostrar todos os brinquedos (`findAll()`)
2. Encontrar um brinquedo específico (`findById()`)
3. Adicionar novos brinquedos, mas só se eles seguirem todas as regras (`create()`)
4. Atualizar informações de brinquedos existentes (`update()`)
5. Remover brinquedos da loja (`delete()`)

E o mais importante: ele protege um brinquedo especial (o usuário com ID 1) que não pode ser modificado ou removido!

Tudo isso é feito com muito cuidado, verificando cada detalhe para garantir que os dados dos usuários estejam sempre corretos e seguros.

Espero que tenha gostado desta viagem pelo mundo dos serviços em Java Spring! 🚀
