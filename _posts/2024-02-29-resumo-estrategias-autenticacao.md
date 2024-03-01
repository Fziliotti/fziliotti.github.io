---
title: Estratégias de autenticação - resumo simplificado
author: fziliotti
date: 2024-02-29 04:33:00 +0800
categories: ["Dev", "Frontend"]
tags: [dev, backend]
---

## Introdução
Estratégias de autenticação são métodos ou técnicas usadas para verificar a identidade de um usuário ou sistema, a fim de conceder acesso a um recurso protegido. Existem várias estratégias de autenticação diferentes que podem ser utilizadas, incluindo:
 
- Autenticação Básica
- Autenticação Baseada em Sessão
- Autenticação Baseada em Token
- Autenticação JWT
- OAuth

Não precisamos necessariamente aprender todas essas estratégias e como implementá-las desde o início. No entanto, é importante conhecer o que são e como funcionam. Isso ajudará a tomar decisões mais informadas ao escolher uma estratégia de autenticação para nossas aplicação.

## Diagramas do roadmap.sh

### Autenticação básica

![Autenticação básica](/assets/img/autenticacao/basic-authentication.png)

### Autenticação baseada em sessão

![Autenticação baseada em sessão](/assets/img/autenticacao/session-authentication.png)

Exemplo prático usando nodejs com express:

```js
const express = require('express');
const session = require('express-session');
const bodyParser = require('body-parser');

const app = express();
const PORT = 3000;

// Middleware para análise de corpo JSON
app.use(bodyParser.json());

// Configuração da sessão
app.use(session({
  secret: 'seu-segredo', // Deve ser uma string única e secreta
  resave: false,
  saveUninitialized: true,
  cookie: { secure: false } // Em produção, configure como true se estiver usando HTTPS
}));

// Rota de login
app.post('/login', (req, res) => {
  const { username, password } = req.body;

  // Simulação de verificação de credenciais (substitua com sua lógica de autenticação real)
  if (username === 'usuario' && password === 'senha') {
    req.session.user = { username }; // Armazene o usuário na sessão
    res.json({ message: 'Login bem-sucedido' });
  } else {
    res.status(401).json({ message: 'Credenciais inválidas' });
  }
});

// Rota protegida
app.get('/recurso-protegido', (req, res) => {
  if (req.session.user) {
    res.json({ message: 'Acesso permitido ao recurso protegido', user: req.session.user });
  } else {
    res.status(401).json({ message: 'Acesso não autorizado' });
  }
});

// Rota de logout
app.post('/logout', (req, res) => {
  req.session.destroy();
  res.json({ message: 'Logout bem-sucedido' });
});

// Inicie o servidor
app.listen(PORT, () => {
  console.log(`Servidor Node.js rodando na porta ${PORT}`);
});


```

### Autenticação baseada em token

![Autenticação baseada em token](/assets/img/autenticacao/token-authentication.png)

### Autenticação com token JWT

![Autenticação com token JWT](/assets/img/autenticacao/jwt-authentication.png)

Exemplo prático com Nodejs:

```js
const express = require('express');
const bodyParser = require('body-parser');
const jwt = require('jsonwebtoken');

const app = express();
const PORT = 3000;
const SECRET_KEY = 'secretpassword'; // Chave secreta para assinar o JWT, substitua por algo mais seguro em produção.

// Middleware para análise de corpo JSON
app.use(bodyParser.json());

// Endpoint para autenticação
app.post('/login', (req, res) => {
  const { username, password } = req.body;

  // Verifique as credenciais (isso é apenas um exemplo, faça a validação adequada em um ambiente real)
  if (username === 'usuario' && password === 'senha') {
    // Crie um token JWT
    const token = jwt.sign({ username }, SECRET_KEY, { expiresIn: '1h' });

    // Retorne o token como resposta
    res.json({ token });
  } else {
    res.status(401).json({ message: 'Credenciais inválidas' });
  }
});

// Middleware para proteger rotas
const authenticateToken = (req, res, next) => {
  const token = req.header('Authorization');

  if (!token) return res.status(401).json({ message: 'Token ausente' });

  jwt.verify(token, SECRET_KEY, (err, user) => {
    if (err) return res.status(403).json({ message: 'Token inválido' });

    req.user = user;
    next();
  });
};

// Rota protegida
app.get('/recurso-protegido', authenticateToken, (req, res) => {
  res.json({ message: 'Acesso permitido ao recurso protegido', user: req.user });
});

// Inicie o servidor
app.listen(PORT, () => {
  console.log(`Servidor Node.js rodando na porta ${PORT}`);
});

```

### Autenticação OAUTH (Open Authentication)

![Autenticação OAUTH (Open Authentication)](/assets/img/autenticacao/oauth.png)


## Referências

- https://roadmap.sh/frontend
- https://www.passportjs.org/ - Middleware famoso para lidar com diferentes tipos de autenticação em Nodejs