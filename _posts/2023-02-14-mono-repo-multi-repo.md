---
title: Anotações sobre monorepos e multirepos
author: fziliotti
date: 2023-02-14 02:33:00 +0800
categorias: [Web]
tags: [web, monorepo, multirepo]
---

# MonoRepo x Multirepo

- Monolito: 1 repositório para 1 projeto.
- Monorepo: 1 repositório para N projetos.
- Multirepo/Polirepo: N repositórios para N projetos.

## Pontos positivos Monorepo:

- Colaboração (vários times podem se ajudar);
- Linters, Testes, Dependências são centralizados. Facilitando manutenção e atualização das aplicações;
- Maior facilidade de rastreio de duplicação de código.

## Pontos negativos Monorepo:

- Um problema no monorepo impacta em todos times/apps;
- Compartilhamento de código (Ao escalar, o compartilhamento de código pode ficar confuso e burocrático);
- Experiência de desenvolvimento (git clone demorado, git log demorado, build demorado);
- Forte acoplamento entre pacotes, dificulta compartilhamento de código. Como por exemplo retirar determinado pacote do monorepo para disponibilizar para outros contextos;
- Testes mal escritos impactam todo o time de engenharia, dado que afetará todo desenvolvedor ou pipeline que executa tais testes.

## Outros pontos de atenção com monorepo:

- Será necessário estruturar o fluxo de entregas e do git, dado que vários times estarão no mesmo repositório;
- Todas as issues e pull requests estarão em um único lugar e teria que pensar em agrupá-las ou diferenciá-las para nâo ficar desoganizado e misturado;
- Gerenciamento de releases será mais complexo e o orquestramento entre times será necessário;
- Deploys mais demorados, etapas do pipeline podem demorar bastante por exemplo para checar os testes, isso exigirá maiores cuidados para aprimorar o processo;
- Débitos técnicos podem incomodar mais que um PoliRepo;
- Autonomia limitada, dado que algumas coisas são padronizadas e decidias. Fugir disso poderia gerar problemas ou não ser recomendado.

---

## Referências

- https://www.toptal.com/front-end/guide-to-monorepos
- https://classic.yarnpkg.com/lang/en/docs/workspaces/
