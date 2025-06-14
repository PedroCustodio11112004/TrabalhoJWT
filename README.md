Tutorial de Uso da Aplicação
Este tutorial explica como usar a aplicação através dos métodos HTTP GET, POST, PUT e DELETE. A aplicação é uma API RESTful que permite o gerenciamento de usuários com autenticação via JWT (JSON Web Token). Os usuários podem ser do tipo USER ou ADMIN, com permissões diferentes.
Pré-requisitos

Postman: Ferramenta para enviar requisições HTTP. Baixe em postman.com.
Aplicação rodando: Certifique-se de que a aplicação está em execução localmente (ex.: http://localhost:8080).

Endpoints Principais

Autenticação:
POST /api/auth/register - Registrar um novo usuário.
POST /api/auth/login - Fazer login e obter um token JWT.


Usuários:
GET /api/user/profile - Obter o perfil do usuário autenticado.
PUT /api/user/profile - Atualizar o perfil do usuário autenticado.


Administradores:
GET /api/admin/users - Listar todos os usuários (somente admin).
PUT /api/admin/users/{id} - Atualizar um usuário pelo ID (somente admin).
DELETE /api/admin/users/{id} - Deletar um usuário pelo ID (somente admin).



Passo a Passo
1. Registrar um Novo Usuário (POST)

Método: POST
URL: http://localhost:8080/api/auth/register
Corpo da Requisição (JSON):{
  "name": "Nome do Usuário",
  "email": "email@exemplo.com",
  "password": "senha123",
  "role": "USER"
}


Resultado Esperado: Resposta com status 200 OK e mensagem "User registered successfully".
Observação: O campo role pode ser "USER" ou "ADMIN".

2. Fazer Login e Obter Token JWT (POST)

Método: POST
URL: http://localhost:8080/api/auth/login
Corpo da Requisição (JSON):{
  "email": "email@exemplo.com",
  "password": "senha123"
}


Resultado Esperado: Resposta com status 200 OK contendo o token JWT, por exemplo:{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}


Observação: Copie o token para usar nas requisições autenticadas.

3. Obter Perfil do Usuário Autenticado (GET)

Método: GET
URL: http://localhost:8080/api/user/profile
Cabeçalho: Authorization: Bearer <token>
Resultado Esperado: Resposta com status 200 OK e os dados do usuário:{
  "id": 1,
  "name": "Nome do Usuário",
  "email": "email@exemplo.com",
  "role": "USER"
}



4. Atualizar Perfil do Usuário Autenticado (PUT)

Método: PUT
URL: http://localhost:8080/api/user/profile
Cabeçalho: Authorization: Bearer <token>
Corpo da Requisição (JSON):{
  "name": "Novo Nome",
  "password": "novaSenha123"
}


Resultado Esperado: Resposta com status 200 OK e mensagem "Profile updated successfully".
Observação: O campo password é opcional. Se fornecido, a senha será atualizada.

5. Listar Todos os Usuários (GET - Apenas Admin)

Método: GET
URL: http://localhost:8080/api/admin/users
Cabeçalho: Authorization: Bearer <token_admin>
Resultado Esperado: Resposta com status 200 OK e uma lista de usuários:[
  {
    "id": 1,
    "name": "Nome do Usuário",
    "email": "email@exemplo.com",
    "role": "USER"
  },
  {
    "id": 2,
    "name": "Admin",
    "email": "admin@exemplo.com",
    "role": "ADMIN"
  }
]


Observação: Apenas usuários com role "ADMIN" podem acessar este endpoint.

6. Atualizar um Usuário pelo ID (PUT - Apenas Admin)

Método: PUT
URL: http://localhost:8080/api/admin/users/{id}
Cabeçalho: Authorization: Bearer <token_admin>
Corpo da Requisição (JSON):{
  "name": "Nome Atualizado",
  "email": "email.atualizado@exemplo.com",
  "role": "USER",
  "password": "novaSenha123"
}


Resultado Esperado: Resposta com status 200 OK e mensagem "User updated successfully".
Observação: O campo password é opcional. Se fornecido, a senha será atualizada.

7. Deletar um Usuário pelo ID (DELETE - Apenas Admin)

Método: DELETE
URL: http://localhost:8080/api/admin/users/{id}
Cabeçalho: Authorization: Bearer <token_admin>
Resultado Esperado: Resposta com status 200 OK e mensagem "User deleted successfully".
Observação: Apenas usuários com role "ADMIN" podem deletar usuários.

Dicas

Token JWT: Inclua o token no cabeçalho de todas as requisições autenticadas no formato Authorization: Bearer <token>.
Permissões: Use um token de admin para acessar os endpoints /api/admin/*.
Erros Comuns:
403 Forbidden: Usuário sem permissão para acessar o recurso (ex.: usuário comum tentando acessar endpoint de admin).
401 Unauthorized: Token ausente, inválido ou expirado.


Validações: Certifique-se de que todos os campos obrigatórios estão presentes nas requisições POST e PUT.

