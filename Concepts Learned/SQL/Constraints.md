# Constraints em SQL: Um Guia para Iniciantes

As constraints (restrições) em SQL são regras aplicadas às colunas de uma tabela para limitar o tipo de dados que podem ser armazenados. Elas ajudam a manter a integridade e precisão dos dados no seu banco de dados. Vamos explorar os principais tipos de constraints:

## 1. PRIMARY KEY (Chave Primária)

- Identifica cada registro em uma tabela de forma única
- Não pode conter valores NULL
- Cada tabela só pode ter uma PRIMARY KEY

```sql
CREATE TABLE Clientes (
    ID INT PRIMARY KEY,
    Nome VARCHAR(100)
);
```

## 2. FOREIGN KEY (Chave Estrangeira)

- Mantém a integridade referencial entre duas tabelas
- Aponta para a PRIMARY KEY em outra tabela
- Impede ações que destruiriam links entre tabelas

```sql
CREATE TABLE Pedidos (
    PedidoID INT PRIMARY KEY,
    ClienteID INT,
    FOREIGN KEY (ClienteID) REFERENCES Clientes(ID)
);
```

## 3. NOT NULL

- Garante que uma coluna não possa conter valores NULL
- Obrigatório para campos essenciais

```sql
CREATE TABLE Produtos (
    ID INT PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL
);
```

## 4. UNIQUE

- Garante que todos os valores em uma coluna sejam diferentes
- Diferente da PRIMARY KEY: pode ter múltiplas colunas UNIQUE e pode conter NULL

```sql
CREATE TABLE Usuarios (
    ID INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE
);
```

## 5. CHECK

- Verifica se os valores em uma coluna satisfazem uma condição específica
- Pode ser aplicado a colunas ou a toda a tabela

```sql
CREATE TABLE Pessoas (
    ID INT PRIMARY KEY,
    Idade INT CHECK (Idade >= 18)
);
```

## 6. DEFAULT

- Define um valor padrão para uma coluna quando nenhum valor é especificado

```sql
CREATE TABLE Pedidos (
    ID INT PRIMARY KEY,
    DataPedido DATE DEFAULT GETDATE()
);
```

## Adicionando Constraints a Tabelas Existentes

Você pode adicionar constraints após a criação da tabela:

```sql
ALTER TABLE Clientes
ADD CONSTRAINT PK_Clientes PRIMARY KEY (ID);

ALTER TABLE Pedidos
ADD CONSTRAINT FK_Pedidos_Clientes
FOREIGN KEY (ClienteID) REFERENCES Clientes(ID);
```

## Removendo Constraints

Para remover uma constraint:

```sql
ALTER TABLE Pedidos
DROP CONSTRAINT FK_Pedidos_Clientes;
```

## Por que usar Constraints?

1. **Integridade dos dados**: Garantem que os dados sejam precisos e confiáveis
2. **Prevenção de erros**: Impedem a inserção de dados inválidos
3. **Relacionamentos**: Mantêm conexões lógicas entre tabelas
4. **Consistência**: Aplicam regras de negócio no nível do banco de dados

As constraints são fundamentais para projetar bancos de dados robustos e confiáveis. À medida que você avança no SQL, entender essas restrições ajudará você a criar estruturas de dados mais eficientes e seguras.
