---
title: "Google Recaptcha: Exemplo prático"
author: fziliotti
date: 2024-02-29 04:33:00 +0800
categories: ["Desenvolvimento"]
tags: [frontend, backend]
---


### Google Recaptcha

O Recaptcha do Google é uma ferramenta que ajuda a proteger seus sites contra atividades maliciosas, fornecendo maior segurança para a aplicação, seja em momentos de login ou em cenários como compra de um produto. 

Neste exemplo, fornecerei um cenário prático do seu uso. Como precisei estudar o assunto, resolvi documentar e compartilhar esse conhecimento que poderá ser aprofundado na documentação do Google de acordo com o caso de uso de sua aplicação.

### Casos de Uso:

**Proteção contra Bots:** Evite ataques automatizados, como preenchimento de formulários em massa, garantindo que apenas usuários reais possam interagir com seus recursos online.

**Prevenção contra Ataques de Força Bruta:** Reforce a segurança de suas páginas de login e formulários sensíveis, protegendo-os contra tentativas repetidas de login por bots.

**Controle de Spam:** Mantenha os comentários do seu blog e outros formulários livres de spam, oferecendo uma barreira eficaz contra bots invasores.

### Implementação


**Front-end**

```html
// Incorporando o Recaptcha no Frontend

// Adicione a API do Recaptcha no seu HTML
<script src="https://www.google.com/recaptcha/api.js"></script>

// Dentro do seu formulário
<form action="/processar-formulario" method="post">
  <!-- Seus campos de formulário aqui -->

  <!-- Adicione o widget Recaptcha -->
  <div class="g-recaptcha" data-sitekey="SEU_SITE_KEY"></div>

  <!-- Botão de Envio -->
  <button type="submit">Enviar</button>
</form>

```

**Back-end com Nodejs:**

```js
// Usando o pacote npm 'express' para gerenciar rotas
const express = require('express');
const bodyParser = require('body-parser');
const axios = require('axios');

const app = express();
const port = 3000;

// Middleware para processar o corpo das requisições
app.use(bodyParser.urlencoded({ extended: true }));

// Rota para processar o formulário
app.post('/processar-formulario', async (req, res) => {
  const recaptchaSecretKey = 'SEU_SECRET_KEY';
  const userResponse = req.body['g-recaptcha-response'];

  // Verificar o Recaptcha usando a API do Google
  const verificationURL = `https://www.google.com/recaptcha/api/siteverify?secret=${recaptchaSecretKey}&response=${userResponse}`;

  try {
    const response = await axios.post(verificationURL);
    const { success, score } = response.data;

    if (success && score >= 0.3) {
      // O Recaptcha foi validado com sucesso e o score é aceitável
      // Continue com o processamento do formulário
      res.send('Formulário processado com sucesso!');
    } else {
      // Falha na validação do Recaptcha ou score abaixo do esperado
      if (!success) {
        res.status(403).send('Erro de validação do Recaptcha. Por favor, tente novamente.');
      } else {
        res.status(403).send('O score do Recaptcha é muito baixo. Você parece ser um bot. Por favor, tente novamente.');
      }
    }
  } catch (error) {
    console.error('Erro ao verificar o Recaptcha:', error);
    res.status(500).send('Erro interno ao processar o formulário. Por favor, tente novamente mais tarde.');
  }
});

// Iniciar o servidor
app.listen(port, () => {
  console.log(`Servidor rodando em http://localhost:${port}`);
});

```

### Considerações

O funcionamento é bem simples:

- Ao incorporar o script do Recaptcha no seu HTML, preferencialmente dentro da tag `<head>`, você permite que o widget apareça nos seus formulários e que o Google avalie a intenção do usuário, além de outras métricas usadas internamente para cálculo do score do usuário.
- No backend, ao receber os dados preenchidos no formulário, você envia a resposta do Recaptcha, incluindo o SECRET_KEY, para a API do Google para verificação.
- A API retorna se a validação foi bem-sucedida e um score, indicando a confiabilidade do usuário.
- Se o Recaptcha validar com sucesso e o score for aceitável (geralmente acima de 0.3), o processamento do formulário continua.

### Para aprofundar mais

- https://developers.google.com/recaptcha/docs/v3 - API de propósito geral
- https://cloud.google.com/recaptcha-enterprise/docs/overview - API voltada para empresas