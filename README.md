# 🚀 API Spring Boot JWT Auth

API construída com **Spring Boot 3.x**, implementando autenticação via JWT, CRUD de usuários e monitoramento.

---

## 📦 Dependências do Projeto

As principais dependências incluídas no `pom.xml`:

✅ **Spring Boot Starter Web** – Construção de APIs RESTful  
✅ **Spring Boot Starter Security** – Autenticação e autorização  
✅ **Spring Boot Starter OAuth2 Resource Server** – Validação de tokens JWT  
✅ **Spring Boot Starter Data JPA** – Persistência de dados  
✅ **H2 Database** – Banco de dados em memória para testes  
✅ **Springdoc OpenAPI** – Geração automática da documentação via Swagger UI  
✅ **Spring Boot DevTools** – Ferramentas para desenvolvimento ágil  
✅ **Lombok** – Redução de código repetitivo  
✅ **Spring Boot Starter Test** – JUnit 5 e Mockito para testes unitários  
✅ **Spring Boot Actuator** – Monitoramento e métricas da API  
✅ **Prometheus** – Coleta de métricas em tempo real

---

## ⚙️ Configuração do Ambiente

### application.yml

Exemplo mínimo de configuração:

```
server:
  port: 8080

spring:
  datasource:
    url: jdbc:h2:mem:testdb
    driver-class-name: org.h2.Driver
    username: sa
    password:
  jpa:
    hibernate:
      ddl-auto: update
  h2:
    console:
      enabled: true

springdoc:
  swagger-ui:
    path: /swagger-ui.html

management:
  endpoints:
    web:
      exposure:
        include: "*"
  metrics:
    export:
      prometheus:
        enabled: true

spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          secret-key: secret-key 
```

## 🛡️ Implementação da API de Autenticação

Endpoints:

POST /account/login → Autenticação e geração de token JWT

POST /account/register → Criação de novos usuários

Validação de tokens JWT feita via:
spring-boot-starter-oauth2-resource-server

Roles:
ROLE_USER
ROLE_ADMIN

## 🔑 Aplicação da Autenticação JWT nos Endpoints CRUD
Endpoints protegidos exigem token JWT

Exemplo protegido:

http
Copiar
Editar
GET /protected
Authorization: Bearer <token>
Controle de acesso por Role:

ROLE_USER → acesso básico

ROLE_ADMIN → operações administrativas (e.g. deletar usuários)

## 📈 Testes de Carga com JMeter
6.1 Instalação do JMeter
Baixar Apache JMeter

Executar:

Windows → jmeter.bat
w
Linux/macOS → jmeter.sh

6.2 Criar Teste de Carga para Login
Criar Thread Group com múltiplos usuários virtuais

Adicionar HTTP Request:
- Método → POST
- URL → /account/login
- Payload → JSON (username, password)

Adicionar Listener:
- Summary Report
- View Results Tree

Métricas importantes:
- Throughput (requisições/segundo)
- Tempo Médio de Resposta
- % de Erros

## 🔗 Endpoints Importantes
Método	Endpoint	Acesso
POST	/account/login	Público
POST	/account/register	Público
GET	/protected	Autenticado
GET	/account/users	Admin/User
DELETE	/account/users/{name}	Admin apenas

## 🧪 Exemplos
```
POST /account/login
Content-Type: application/json

{
    "username": "admin",
    "password": "123"
}
```

Resposta:
"eyJhbGciOiJIUzI1NiIsInR..."
