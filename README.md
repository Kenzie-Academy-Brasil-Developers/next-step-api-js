<h1 align="center">
  Next Step - API
</h1>

<p align = "center">
<h2 align="center">
  Componentes do Grupo  
</h2>

									Emerson Gomes - PO

									Luan Marchi - QA

									Matheus Sudré - TL/SM

									Carlos Blanco - QA

</p>

<p align = "center">
Este é o backend da aplicação Next Step - Um aplicativo de portfólios voltado para a área da tecnologia! O objetivo dessa aplicação é simular uma API e atráves dela construir um frontend de qualidade em grupo, utilizando o que foi ensinado no terceiro módulo do curso (M3) - E desenvolver hard skills e soft skills.
</p>

<blockquote align="center">“As raízes dos estudos são amargas, mas seus frutos são doces. - Aristóteles”</blockquote>

<p align="center">
  <a href="#endpoints">Endpoints</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</p>

## **Endpoints**

A API tem um total de (editar depois) endpoints, sendo em volta principalmente do usuário - podendo cadastrar/editar seu perfil, tecnologias que estuda e trabalhos realizados. <br/>

O url base da API é https://next-step-api-js-my-production.up.railway.app


<h2 align ='center'> Listando usuário </h2>

Nessa aplicação o usuário necessita fazer login ou se cadastrar para ter acesso somente aos dados que lhe-pertence.

<h2 align ='center'> Criação de usuário </h2>

`POST /users - FORMATO DA REQUISIÇÃO`

```json
{  
  "name": "Matheus Araújo",
  "email": "matheus@gmail.com",
  "password": "Teste@123",
  "confirmPassword": "Teste@123",
  "image": "https://avatars.githubusercontent.com/u/100591242?s=400&u=4959ce9ec57cec5a891d320ac12c5fbf1214163c&v=4",
  "bio": "Lorem ipsum dolor emet,Lorem ipsum dolor emet,Lorem ipsum dolor emet" 
}
```

Caso dê tudo certo, a resposta será assim:

`POST /users - FORMATO DA RESPOSTA - STATUS 201`

```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hdGhldXNAZ21haWwuY29tIiwiaWF0IjoxNjYyMTI0ODA4LCJleHAiOjE2NjIxMjg0MDgsInN1YiI6IjIifQ.VzKejBcOImVccOttUBwfr-GNXTw04S3CbnySkCQaAT8",
	"user": {
		"email": "matheus@gmail.com",
		"name": "Matheus Araújo",
		"confirmPassword": "Teste@123",
		"image": "https://avatars.githubusercontent.com/u/100591242?s=400&u=4959ce9ec57cec5a891d320ac12c5fbf1214163c&v=4",
		"bio": "Lorem ipsum dolor emet,Lorem ipsum dolor emet,Lorem ipsum dolor emet",
		"id": 2
	}
}
```

<h2 align ='center'> Possível erro no cadastro</h2>

Caso você acabe errando e mandando algum campo errado, a resposta de erro será assim:
No exemplo a requisição foi feita faltando o campo "contact" e "course_module".

`POST /users - `
` FORMATO DA RESPOSTA - STATUS 400`

Email já cadastrado:

`POST /users - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
{
  "status": "error",
  "message": "Email already exists"
}
```

<h2 align = "center"> Login </h2>

`POST /login - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "matheus@gmail.com",
  "password": "Teste@123",
}
```

Caso dê tudo certo, a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 201`

```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hdGhldXNAZ21haWwuY29tIiwiaWF0IjoxNjYyMTI1MjI2LCJleHAiOjE2NjIxMjg4MjYsInN1YiI6IjIifQ.isSqp4hSZrYxBbfkm9xO9zrwIqj58V7dBtf8CMS9oAw",
	"user": {
		"email": "matheus@gmail.com",
		"name": "Matheus Araújo",
		"confirmPassword": "Teste@123",
		"image": "https://avatars.githubusercontent.com/u/100591242?s=400&u=4959ce9ec57cec5a891d320ac12c5fbf1214163c&v=4",
		"bio": "Lorem ipsum dolor emet,Lorem ipsum dolor emet,Lorem ipsum dolor emet",
		"id": 2
	}
}
```

Com essa resposta, vemos que temos duas informações, o user e o accessToken respectivo, dessa forma você pode guardar o accessToken e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Buscar Perfil do usuário logado (token) </h2>

`GET /users/id - FORMATO DA REQUISIÇÃO`

<blockquote>Na requisição apenas é necessário o accessToken e o Id do usuário</blockquote>

<br>

`GET /users/id - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"email": "matheus@gmail.com",
	"password": "$2a$10$f.hewy3JIPxipESL82c81.6.S1X/s2aOS0csDSkGnfHpOFGMnlW7W",
	"name": "Matheus Araújo",	
	"image": "https://avatars.githubusercontent.com/u/100591242?s=400&u=4959ce9ec57cec5a891d320ac12c5fbf1214163c&v=4",
	"bio": "Lorem ipsum dolor emet,Lorem ipsum dolor emet,Lorem ipsum dolor emet",
	"id": 2
}
```

<h2 align ='center'> Criar tecnologias para o seu perfil </h2>

`POST /techs - FORMATO DA REQUISIÇÃO`

```json (Alterar depois)
{
	"name": "Kenzie Hub",
	"info": "controle de tecnologias",
	"libs": "yup,hookForm",
	"userId": 2,
	"nivel": "Iniciante"
}
```

1. O campo - "nivel" deve receber respectivamente os 3 níveis de habilidade:
   - "Iniciante"
   - "Intermediário"
   - "Avançado"

você dar update em quanto você avançou nas tecnologias que já está no seu perfil. Utilizando este endpoint:

`PATCH /techs/tech_id - FORMATO DA REQUISIÇÃO`

```json
{
  "status": "Avançado"
}
```

Também é possível deletar uma tecnologia, utilizando este endpoint:

`DELETE /techs/tech_id`

```
Não é necessário um corpo da requisição.
```

<h2 align ='center'> Criar trabalhos para o seu perfil </h2>

Da mesma forma de criar tecnologias, conseguimos criar projetos, dessa forma:

`POST /projects - FORMATO DA REQUISIÇÃO`

```json
{
  "title": "KenzieHub",
  "description": "I was the backend developer of this project, and i did it using Typescript and NodeJS",
  "deploy_url": "https://kenziehub.me",
  "userId": 2
}
```

Conseguimos atualizar o titulo, a descrição ou o deploy_url, qualquer uma das informações do respectivo trabalho.
Utilizando este endpoint:

`PATCH /projects/project_id - FORMATO DA REQUISIÇÃO`

```json
{
  "title": "KenzieHub Atualizado",
  "description": "Nova descrição."
}
```

Também é possível deletar um trabalho do seu perfil, utilizando este endpoint:

`DELETE /projects/project_id`

```
Não é necessário um corpo da requisição.
```

<h2 align ='center'> Atualizando os dados do perfil </h2>

Assim como os endpoints de tecnologias e trabalhos, nesse precisamos estar logados, com o token no cabeçalho da requisição. Estes endpoints são para atualizar seus dados como, foto de perfil, nome, ou qualquer outra informação em relação ao que foi utilizado na criação do usuário.

Endpoint para atualizar a foto de perfil:

`PATCH /users/user_id - FORMATO DA REQUISIÇÃO`

```multipart
avatar: <Arquivo de imagem>
```
