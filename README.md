# Api-go

API REST desenvolvida em Go como base para um CRUD de produtos.

O projeto utiliza Gin para gerenciamento das rotas HTTP, PostgreSQL como banco de dados e uma organizacao simples em camadas, separando responsabilidades entre controller, usecase, repository, model e conexao com banco.

## Tecnologias

- Go
- Gin
- PostgreSQL
- Docker Compose

## Estrutura

```text
.
|-- cmd/
|   `-- main.go
|-- controller/
|   `-- product_controller.go
|-- db/
|   `-- conn.go
|-- model/
|   `-- product.go
|-- repository/
|   `-- product_repository.go
|-- usecase/
|   `-- product_usercase.go
|-- docker-compose.yml
|-- go.mod
`-- go.sum
```

## Como executar

### 1. Subir o banco de dados

Na raiz do projeto, execute:

```bash
docker compose up -d
```

O PostgreSQL sera iniciado via Docker Compose. As configuracoes locais de conexao estao definidas nos arquivos do projeto.

### 2. Criar a tabela de produtos

Crie a tabela utilizada pela rota de listagem:

```sql
CREATE TABLE product (
    id SERIAL PRIMARY KEY,
    product_name VARCHAR(255) NOT NULL,
    price NUMERIC(10, 2) NOT NULL
);
```

Opcionalmente, insira alguns registros para teste:

```sql
INSERT INTO product (product_name, price)
VALUES
    ('Produto 1', 10.90),
    ('Produto 2', 25.50);
```

### 3. Executar a API

```bash
go run ./cmd
```

A API sera iniciada na porta `3333`.

## Rotas

### Health check

```http
GET /ping
```

Resposta:

```json
{
  "message": "pong"
}
```

### Listar produtos

```http
GET /products
```

Resposta:

```json
[
  {
    "id_product": 1,
    "name": "Produto 1",
    "price": 10.9
  }
]
```

## Status do projeto

Este projeto esta em desenvolvimento.

Atualmente, a estrutura inicial da API esta criada e a listagem de produtos ja esta disponivel:

- `GET /products`

Proximas operacoes previstas para completar o CRUD:

- Criar produto
- Buscar produto por ID
- Atualizar produto
- Remover produto
