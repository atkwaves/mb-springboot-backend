# MB Spring Boot Backend

Projeto backend desenvolvido com Spring Boot e banco de dados PostgreSQL. A aplicação expõe uma API RESTful para gerenciamento 
de produtos, com operações de CRUD estruturadas com base no modelo de Maturidade de Richardson (nível 3), utilizando URIs bem 
definidas, verbos HTTP adequados e HATEOAS para enriquecimento das respostas com hipermídia.

## Tecnologias utilizadas

- Java 17
- Spring Boot 3.4.2
- Spring Data JPA
- Spring Web
- Spring HATEOAS
- Jakarta Bean Validation
- PostgreSQL
- Maven

## Como executar o projeto

Pré-requisitos:
- Java 17+
- PostgreSQL
- Maven

1. Clonar o repositório:
```
git clone https://github.com/atkwaves/mb-springboot-backend.git
```

2. Acessar a pasta do projeto:
```
cd mb-springboot-backend
```

3. Criar o banco de dados no PostgreSQL:
```sql
CREATE DATABASE springboot_db;
```

4. Definir as variáveis de ambiente `DB_USERNAME` e `DB_PASSWORD` com as credenciais do banco.

5. Executar a aplicação:
```
./mvnw spring-boot:run
```

Ou executar a classe `MbSpringbootBackendApplication` pela IDE.

## Configuração do banco de dados

Configurações definidas no arquivo `application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/springboot_db
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
```
> **Observação**: A propriedade `spring.jpa.hibernate.ddl-auto=update` está configurada para que o schema do banco de dados 
> seja gerado e atualizado automaticamente com base nas entidades JPA. Essa configuração é adequada para ambientes de desenvolvimento.

## Endpoints da API

### POST `/products`   
Cadastrar um novo produto.  

**Corpo da requisição:**

```json
{
  "name": "Notebook",
  "value": 3500.00
}
```
### GET `/products`  
Listar todos os produtos.

### GET `/products/{id}`  
Consultar um produto pelo ID.

### PUT `/products/{id}`  
Atualizar os dados de um produto existente.  

**Corpo da requisição:**

```json
{
  "name": "Notebook atualizado",
  "value": 3900.00
}
```

### DELETE `/products/{id}`  
Excluir um produto pelo ID.

## Validação de dados

A entrada de dados nos endpoints utiliza Jakarta Bean Validation. O DTO `ProductRecordDto` aplica as seguintes restrições:

- `name`: obrigatório (`@NotBlank`)
- `value`: obrigatório (`@NotNull`)

```java
public record ProductRecordDto(
    @NotBlank String name,
    @NotNull BigDecimal value
) {}
```

## Estrutura de pacotes

- `controllers` — Expõe os endpoints da API.
- `dtos` — Define os objetos de entrada (DTOs) com validação.
- `model` — Contém a entidade JPA que representa o produto.
- `repositories` — Define a interface do repositório com Spring Data JPA.

## Licença

Projeto licenciado sob a licença MIT.