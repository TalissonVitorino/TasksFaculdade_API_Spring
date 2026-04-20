# Tasks API (Spring Boot)

API REST simples para gerenciamento de tarefas, desenvolvida com `Spring Boot`, `Spring Data JPA` e banco relacional.

## O que esta API faz

A API permite realizar operações completas de CRUD em tarefas:

- Criar uma nova tarefa
- Listar todas as tarefas
- Buscar tarefa por ID
- Atualizar tarefa existente
- Remover tarefa

### Modelo de dados (`Task`)

Cada tarefa possui os campos:

- `id` (`Long`) — gerado automaticamente
- `title` (`String`) — obrigatório
- `description` (`String`) — opcional
- `completed` (`boolean`) — indica se foi concluída

## Como usar

### Pré-requisitos

- `Java 17+`
- `Gradle` (ou usar o wrapper `./gradlew`)

### Executar localmente

```bash
./gradlew bootRun
```

Por padrão, a aplicação sobe em:

- `http://localhost:8080`

Base dos endpoints:

- `http://localhost:8080/tasks`

## Endpoints

### 1) Listar tarefas

- Método: `GET`
- URL: `/tasks`

Exemplo:

```bash
curl -X GET http://localhost:8080/tasks
```

### 2) Buscar tarefa por ID

- Método: `GET`
- URL: `/tasks/{id}`

Exemplo:

```bash
curl -X GET http://localhost:8080/tasks/1
```

### 3) Criar tarefa

- Método: `POST`
- URL: `/tasks`
- Body (JSON):

```json
{
  "title": "Estudar Spring",
  "description": "Revisar controllers e services",
  "completed": false
}
```

Exemplo:

```bash
curl -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Estudar Spring",
    "description": "Revisar controllers e services",
    "completed": false
  }'
```

### 4) Atualizar tarefa

- Método: `PUT`
- URL: `/tasks/{id}`
- Body (JSON):

```json
{
  "title": "Estudar Spring Boot",
  "description": "Atualizar documentação",
  "completed": true
}
```

Exemplo:

```bash
curl -X PUT http://localhost:8080/tasks/1 \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Estudar Spring Boot",
    "description": "Atualizar documentação",
    "completed": true
  }'
```

### 5) Deletar tarefa

- Método: `DELETE`
- URL: `/tasks/{id}`

Exemplo:

```bash
curl -X DELETE http://localhost:8080/tasks/1
```

## Códigos de resposta esperados

- `200 OK` — sucesso em consultas/atualização
- `201 Created` — tarefa criada
- `204 No Content` — tarefa removida
- `404 Not Found` — tarefa não encontrada

## Como melhorar esta API (visão mais sênior)

Aqui estão evoluções importantes para produção:

1. **Validação de entrada**
   - Adicionar `@Valid` no controller e anotações como `@NotBlank` no `title`.
2. **Tratamento global de exceções**
   - Criar `@ControllerAdvice` para padronizar erros (JSON com timestamp, status e mensagem).
3. **DTOs e separação de camadas**
   - Evitar expor entidade JPA direto na API; usar `TaskRequest` e `TaskResponse`.
4. **Paginação e filtros**
   - Implementar paginação no `GET /tasks` (`Pageable`) e filtros por status.
5. **Observabilidade**
   - Logs estruturados, métricas (Micrometer/Actuator) e tracing.
6. **Documentação da API**
   - Integrar Swagger/OpenAPI para documentação interativa.
7. **Segurança**
   - Adicionar autenticação/autorização com Spring Security + JWT.
8. **Testes mais robustos**
   - Cobrir cenários de erro, contratos de API e testes de integração com banco de teste.

## Estrutura principal do projeto

```text
src/main/java/com/talisson/tasks
├── controller/TaskController.java
├── model/Task.java
├── repository/TaskRepository.java
├── service/TaskService.java
└── TasksApplication.java
```
