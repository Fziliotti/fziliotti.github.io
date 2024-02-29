---
title: Anotações sobre github
author: fziliotti
date: 2023-02-22 04:33:00 +0800
categorias: ["Dev", "Git"]
tags: [github, tools]
---

## Para verificar os comandos existentes:
- `git help`
- `git __COMAND__ -help`
 
## Para iniciar um repositório git:

- `git init`


## Para visualizar as alterações e diferenças entre commits:

- `git diff _commit1_ _commit2_`, em que X e Y são os identificadores dos commits.


## Para visualizar o histórico do git:

- Instalar o `git history` no vscode
- Apertar `ctrl + shift + P` e digitar: "git log"


## Como atualizar sua branch?

Se você estiver atualizando sua branch pegando as coisas da branch master use `git pull --rebase`

Se você terminou a feature na branch e quer jogar para master, use `git pull` ou `git merge`


### Rebase X Merge

- No git Merge, um novo commit de merge será criado. Isso é interessante para momentos em que novas funcionalidades serão inseridas, demarcando o momento exato da atualização.
- No `git pull --rebase` o histórico do commit ficará mais limpo, sem o novo commit de merge. Os commits que estão feitos localmente, ficarão no topo do histórico de commits.


## Configurar upstream
- `git branch --set-upstream-to=origin/master __branch__`

> Esse comando vai configurar o upstream que será a branch master. Dessa forma, para comandos diretos como `git pull e git push` a referência da branch que será usada como a referencia para as atualizações será a master.

## Como editar commits com erros?

Para um cenário em que você descreveu um commit da forma errada, você pode editar o commit usando o comando `git commit --amend` que vai abrir a interface do git e você pode editar as informações de commit.

Se você quiser incluir determinada alteração que ficou faltando, você utiliza o mesmo processo. Pode utilizar o `git show __commit-id__` para validar se as alterações estão corretas.

## Como juntar dois commits em um só?

Para juntar dois commits diferentes em um único commit, você pode usar o `git rebase -i HEAD~3` e de maneira interativa, escolher o que você quer fazer com os commits.

## Como reverter commits?

- O comando `git revert __id-commit__` vai ser responsável por reverter as alterações feitas de determinado commit, de maneira rápida.
  - É importante destacar que esse comando irá criar um novo commits de reversão. Sem apagar o antigo commit do histórico.
  - Como esse comando não vai alterar o histórico, ele é indicado e recomendado na maioria das vezes. Principalmente para não atrapalhar e gerar problemas em outras branchs que podem apresentar conflitos ao serem atualizadas.

- Outra técnica para reverter commits é utilizar o `git reset --hard __commit-id__` e também o `git reset --soft __commit-id__`
  - Interessante para branchs próprios, diferentes de branchs principais como master e qa por exemplo.


## Habilitar o auto-correct do Git

Para auxiliar em momentos que você digita errado os comandos do git, como `git committ` ou `git stattus`, você pode ativar uma configuração global do git para auxiliar nisso.

O comando é `git config --global help.autocorrect 1`

## Extensões do VSCODE

Além dos aliases configurados para o git presentes nessa postagem que fiz dias atrás, algumas extensões para o git são bastante úteis no dia a dia:


*Git Blame*

- Essa extensão do vscode vai facilitar a identificação de quem fez as últimas modificações no código.

*Git History* 

- Essa entensão é muito boa para mostrar o histórico de commits de um repositório, facilitando na organização do projeto, na identificação de pontos de mudanças e bugs.
- A organização ficará em linha cronológica, com as ramificações, caso existam, dos outras branchs existentes no repositório.

*Git Lens*

- Essa é uma extensão bem completa que oferecem uma gama de recursos para o vscode. Recursos como mostrar histórico e identificar os últimos alteradores das linhas de códigos como o Git Blame, facilita tambem na navegação entre branchs e commits e Histórico de commits de maneira mais visual. A extensão é bem completa e vale a pena testar.


## Referências

- [Commitlint](https://github.com/conventional-changelog/commitlint) - Ferramenta para validar mensagens de commit.
- [Conventional-commits](https://www.conventionalcommits.org/en/v1.0.0/) - especificação famosa para convencionar commits facilitando e padronizando o desenvolvimento

