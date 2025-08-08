# 🧩 Login Auth API – Spring Boot

Este é o backend da aplicação de autenticação feita com Angular + Spring Boot. Ele fornece endpoints RESTful para **cadastro**, **login** e **validação de autenticação JWT** com proteção de rotas e integração total com o frontend.

---

## ⚙️ Tecnologias Utilizadas

- Java 17+
- Spring Boot 3+
- Spring Security
- JWT (com `java-jwt` da Auth0)
- H2 Database (em memória)
- Maven

---

## 🧠 Funcionalidades

- Registro de novos usuários (`/auth/register`)
- Login com retorno de JWT (`/auth/login`)
- Proteção de endpoints com `Bearer Token`
- Validação de token com filtro customizado
- Retorno do nome do usuário e token
- CORS habilitado para o frontend Angular (`http://localhost:4200`)

---

## 🧪 Testar a API Localmente

### 1. Clonar o projeto

```bash
git clone https://github.com/PedroRSilveira/app-login-springboot.git
cd app-login-springboot
```

### 2. Executar com Maven

```bash
./mvnw spring-boot:run
```

A aplicação iniciará em `http://localhost:8080`.

### 3. Endpoints disponíveis

| Método | Endpoint         | Autenticação | Descrição                  |
|--------|------------------|--------------|----------------------------|
| POST   | `/auth/register` | ❌           | Cadastra novo usuário      |
| POST   | `/auth/login`    | ❌           | Realiza login e gera token |
| GET    | `/user`          | ✅ Bearer    | Endpoint protegido         |

---


## 📡 Integração com Frontend

Este backend funciona em conjunto com o frontend Angular que pode ser encontrado aqui:

👉 [Frontend do Projeto - Angular](https://github.com/PedroRSilveira/app-login-angular)

---

## 🔐 Segurança com Spring Security + JWT

### 📌 Filtro personalizado

- O `SecurityFilter` intercepta requisições e valida o token.
- Usuário autenticado é armazenado no `SecurityContext`.

### 📌 Geração e Validação do Token

- Token criado com `java-jwt` (Auth0)
- Expira após 2 horas
- Assinado com segredo definido em `application.properties`

```properties
api.security.token.secret=my-secret-key
```

---

## 🔐 Como funciona a autenticação?

1. **Cadastro:** O usuário é salvo com senha criptografada (BCrypt).
2. **Login:** Token JWT é gerado e enviado ao cliente.
3. **Requisições futuras:** Token deve ser enviado no header `Authorization`.
4. **Filtro de segurança:** Token é validado e usuário autenticado para acessar rotas protegidas.

---

## 🧰 Banco de Dados (H2)

- Base de dados em memória (`jdbc:h2:mem:testdb`)
- Nenhuma configuração externa necessária
- Inicia limpa a cada vez que a aplicação é reiniciada

Acesse o console (opcionalmente habilitável):

```
http://localhost:8080/h2-console
JDBC URL: jdbc:h2:mem:testdb
```

---

## 🧾 Exemplo de Requisições

### 📬 Cadastro

```http
POST /auth/register
Content-Type: application/json

{
  "name": "Pedro",
  "email": "pedro@email.com",
  "password": "123456"
}
```

### 📬 Login

```http
POST /auth/login
Content-Type: application/json

{
  "email": "pedro@email.com",
  "password": "123456"
}
```

**Resposta:**

```json
{
  "name": "Pedro",
  "token": "eyJhbGciOiJIUzI1..."
}
```

### ✅ Requisição protegida

```http
GET /user
Authorization: Bearer eyJhbGciOiJIUzI1...
```

---

## 📝 Licença

Distribuído sob a licença MIT. Consulte `LICENSE` para mais informações.
