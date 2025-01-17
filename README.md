# zenith - Sistema de Gestão Maçônica

Sistema de gestão para administração dos membros de uma associação maçônica, desenvolvido em Java com Spring Boot.

## Autor
Marcos Ribeiro

## Tecnologias Utilizadas

- Java 17
- Spring Boot 3.2.0
- MySQL 5.7
- Docker
- Maven
- JWT para autenticação
- Spring Security

## Pré-requisitos

- Docker e Docker Compose
- Java 17 JDK
- Maven 3.6+

## Configuração e Instalação

1. Clone o repositório:
```bash
git clone [URL_DO_REPOSITORIO]
cd zenith
```

2. Build do projeto:
```bash
mvn clean package -DskipTests
```

3. Iniciar os containers Docker:
```bash
docker-compose up -d
```

O sistema estará disponível em `http://localhost:8080`

## Estrutura do Banco de Dados

O sistema utiliza MySQL 5.7 com as seguintes tabelas:
- users: Usuários do sistema
- roles: Papéis/funções dos usuários
- user_roles: Relacionamento entre usuários e papéis
- members: Membros da associação

## Usuários Padrão

O sistema é inicializado com os seguintes usuários (todos com senha: password123):

| Username    | Role       | Email                    |
|------------|------------|--------------------------|
| admin      | ADMIN      | admin@loja.com.br        |
| veneravel  | VENERAVEL  | veneravel@loja.com.br    |
| tesoureiro | TESOUREIRO | tesoureiro@loja.com.br   |
| secretario | SECRETARIO | secretario@loja.com.br   |
| chanceler  | CHANCELER  | chanceler@loja.com.br    |

## API Endpoints

### Autenticação

```
POST /api/auth/login
```
Request body:
```json
{
    "username": "admin",
    "password": "password123"
}
```

### Gestão de Membros

| Método | Endpoint | Descrição | Roles Permitidas |
|--------|----------|-----------|------------------|
| POST | `/api/members` | Criar novo membro | ADMIN, SECRETARIO |
| GET | `/api/members/{id}` | Buscar membro por ID | ADMIN, VENERAVEL, SECRETARIO |
| GET | `/api/members` | Listar todos os membros | ADMIN, VENERAVEL, SECRETARIO |
| PUT | `/api/members/{id}` | Atualizar membro | ADMIN, SECRETARIO |
| DELETE | `/api/members/{id}` | Excluir membro | ADMIN |
| GET | `/api/members/status?ativo=true` | Listar membros por status | ADMIN, VENERAVEL, SECRETARIO |

### Exemplo de Requisição para Criar/Atualizar Membro

```json
{
    "name": "José Silva",
    "cim": "CIM123",
    "grau": "Mestre",
    "dataNascimento": "1975-05-15",
    "cpf": "123.456.789-00",
    "rg": "12.345.678-9",
    "profissao": "Engenheiro",
    "endereco": "Rua das Acácias, 123",
    "cidade": "São Paulo",
    "estado": "SP",
    "cep": "01234-567",
    "telefone": "(11) 98765-4321",
    "email": "jose.silva@email.com",
    "dataIniciacao": "2010-03-20",
    "observacoes": "Membro ativo",
    "ativo": true
}
```

## Segurança

- Autenticação via JWT Token
- Senhas criptografadas com BCrypt
- Controle de acesso baseado em roles
- Validação de dados de entrada
- Proteção contra duplicidade de CIM e CPF

## Ambiente de Desenvolvimento

Para executar o projeto em ambiente de desenvolvimento:

1. Configure o banco de dados MySQL:
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/zenith?useSSL=false&allowPublicKeyRetrieval=true
    username: root
    password: root
```

2. Execute a aplicação:
```bash
mvn spring-boot:run
```

## Testes da API

Você pode testar a API usando curl ou Postman. Exemplo de login:

```bash
curl -X POST http://localhost:8080/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"password123"}'
```

Para outras requisições, use o token JWT retornado no header Authorization:

```bash
curl -X GET http://localhost:8080/api/members \
  -H "Authorization: Bearer ${TOKEN}"
```

## Suporte

Para suporte ou dúvidas, entre em contato através do email: [seu-email]

## Licença

[Tipo de Licença]
#   z e n i t h - a p i - s p r i n g  
 #   z e n i t h - a p i - s p r i n g  
 