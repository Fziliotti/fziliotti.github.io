---
title: Anotações sobre Graphql
author: fziliotti
date: 2023-02-22 04:33:00 +0800
categorias: ["Dev"]
tags: [graphql, web]
---

## Introdução

GraphQL é uma linguagem de consulta para APIs criada pelo Facebook em 2012 e que se tornou uma especificação aberta em 2015.

Ela permite que os clientes das APIS especifiquem exatamente o que desejam obter em suas consultas, reduzindo bastante a quantidade de informações desnecessárias que um endpoint no formato das APIs REST tradicionais geralmente podem trazer.

## Recursos básicos

Consulta de informações de um usuário com as consultas.

Adição e modificação de recurso por meio das Mutations.

## Projeto backend + frontend.

### Back-end

Dependencies:
- apollo-server
- class-validator
- graphql
- reflect-metadata
- type-graphql

devDependencies:
- @types/node
- ts-node-dev
- typescript

### Front-end
dependencies:
- @apollo/client
- graphql
- react
- react-dom

devDependencies:
- @types/react
- @types/react-dom
- @vitejs/plugin-react
- typescript
- vite

> O projeto foi baseado em um projeto da Rockeseat e gostei bastante das tecnologias, apesar de ter ficado um pouco superficial em termos de funcionalidades. 

## Próximos passos
Aos pouco pretendo melhorar o projeto com funcionalidades mais complexas com as tecnologias.