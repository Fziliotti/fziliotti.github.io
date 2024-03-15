---
title: "Arquitetura na web - um breve overview"
author: fziliotti
date: 2024-02-29 04:33:00 +0800
categories: ["Desenvolvimento"]
tags: [frontend]
---

## Introdução

Recentemente estou auxiliando em entrevistas para engenheiros frontend, principalemnte para plenos e seniores. Deixarei anotando aqui, diversos pontos que permeiam o assunto de arquitetura de aplicações web.


## Arquitetura:

## O que é Arquitetura?

Em um contexto geral, arquitetura refere-se à estrutura fundamental ou organização subjacente de um sistema ou entidade. Quando aplicado a sistemas de software, como aplicativos web, a arquitetura descreve a maneira como os diferentes componentes do sistema interagem entre si e com o ambiente externo.

A arquitetura de software é uma representação abstrata do sistema que define sua estrutura, comportamento, e interações. Ela geralmente inclui aspectos como:

1. **Componentes e Módulos:** Os blocos de construção do sistema, que podem incluir módulos de software, bibliotecas, serviços, etc.

2. **Conectores:** Os mecanismos que permitem a comunicação e interação entre os componentes, como APIs, protocolos de comunicação, barramentos de eventos, etc.

3. **Padrões de Integração:** Conjuntos de diretrizes ou abordagens para integrar diferentes partes do sistema, garantindo coesão e baixo acoplamento.

4. **Distribuição:** Se o sistema é distribuído ou monolítico, e como os diferentes componentes são distribuídos fisicamente (por exemplo, em diferentes servidores, contêineres, etc.).

5. **Escalabilidade e Desempenho:** Considerações sobre como o sistema pode crescer para atender a demandas crescentes de usuários, bem como garantir a eficiência e o desempenho.

6. **Segurança:** Mecanismos para proteger o sistema contra ameaças externas e garantir a integridade, confidencialidade e disponibilidade dos dados.

7. **Persistência de Dados:** Como os dados são armazenados, acessados e manipulados pelo sistema, incluindo estruturas de banco de dados, caches, etc.

8. **Aspectos Não-Funcionais:** Requisitos que não estão diretamente relacionados às funcionalidades do sistema, como disponibilidade, confiabilidade, manutenibilidade e usabilidade.

Em resumo, a arquitetura de software é essencial para garantir que um sistema de software seja robusto, flexível, escalável e atenda aos requisitos funcionais e não-funcionais definidos para ele. É a base sobre a qual todo o desenvolvimento e manutenção de software são construídos.


## Arquitetura na web:

A arquitetura de uma aplicação web engloba:

1. **Frontend e Backend:** A separação de responsabilidades entre a interface do usuário (frontend) e a lógica de negócios e dados (backend).

2. **Protocolos de Comunicação:** Como os dados são transmitidos entre o cliente e o servidor, geralmente usando protocolos como HTTP(S).

3. **Modelo de Solicitação-Resposta:** A maneira como as solicitações do cliente são tratadas e as respostas correspondentes são retornadas pelo servidor.

4. **Roteamento e Navegação:** O mecanismo que permite aos usuários navegar entre diferentes páginas ou estados de uma aplicação web.

5. **Persistência de Dados:** Como os dados são armazenados e acessados, incluindo o uso de bancos de dados, caches e armazenamento em cache do navegador.

6. **Segurança na Web:** Medidas para proteger a aplicação web contra ameaças como ataques de injeção, cross-site scripting (XSS), e outros tipos de ataques.

7. **Escalabilidade e Desempenho:** A capacidade do sistema de lidar com um aumento no número de usuários e garantir uma boa experiência de usuário, incluindo estratégias de cache e otimização de carregamento.

8. **Integração de Serviços Externos:** Como a aplicação web se integra a serviços externos, como APIs de terceiros.

## No contexto React:

**Padrões de Arquitetura: **
- Arquitetura MVC (Model-View-Controller)
- Arquitetura MVVM (Model-View-ViewModel)
- Arquitetura Flux (comumente usado em aplicações React)

**SPA (Single Page Application):**
- Conceitos básicos de como funciona uma SPA
- Frameworks populares para criar SPAs (React, Angular, Vue.js)
- Roteamento em SPAs (React-Router)

**APIs RESTful:**
- Princípios de design de APIs RESTful
- CRUD Operations (Create, Read, Update, Delete) em APIs REST
- Consumo de APIs REST em aplicações frontend

**Gerenciamento de Estado:**
- Redux (ou outras bibliotecas de gerenciamento de estado como Vuex para Vue.js)
- Context API (no contexto do React)
- Reactive State Management (por exemplo, usando RxJS)

**Performance e Otimização:**
- Otimização de carregamento de página
- Otimização de renderização
- Lazy loading de recursos
- Estratégias de cache

**Segurança:**
- XSS (Cross-Site Scripting) e como evitá-lo
- CSRF (Cross-Site Request Forgery) e como evitá-lo
- Autenticação e autorização em aplicações web

**Arquitetura de Componentes:**
- Componentização e reutilização de componentes
- Atomic Design ou outras abordagens para organizar componentes

**Testes:**
- Testes unitários para componentes frontend
- Testes de integração
- Ferramentas e bibliotecas de teste (Jest, Mocha, Jasmine, etc.)
  
**Ferramentas de Desenvolvimento:**
- Bundlers (Webpack, Parcel)
- Task Runners (Gulp, Grunt)
- Dependency Managers (npm, Yarn)
  
**DevOps e Implantação:**
- Continuous Integration (CI) e Continuous Deployment (CD)
- Docker e contêineres
- Implantação em serviços de hospedagem (AWS, Firebase, Netlify)
  
**Padrões de Design e UX/UI:**
- Princípios de design responsivo
- Acessibilidade web
- Boas práticas de design de interface do usuário

**Monitoramento e Logging:**
- Ferramentas de monitoramento de desempenho (como Google Analytics)
- Logging e captura de erros

## Referências

- Para aprofundar no tema de Software Design e Arquitetura, recomendo o link:
  - https://roadmap.sh/software-design-architecture