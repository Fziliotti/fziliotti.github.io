---
title: Minhas configurações de ambiente de desenvolvimento
author: fziliotti
date: 2023-02-22 04:33:00 +0800
categorias: ["Dev", "Setup"]
tags: [setup, configs]
---

# Configurações pessoais do ambiente de desenvolvimento

Configuração do terminal:

Uma recomendação seria a configuração do oh-my-zsh com spaceship e algum tema personalizado:
- https://blog.rocketseat.com.br/terminal-com-oh-my-zsh-spaceship-dracula-e-mais/

---

Configuração do VSCode:

Com a extensão eslint instalada, uma configuração legal que eu faço é habilitar a formatação sugerida pelo eslint ao salvar o arquivo ou colar um código novo.

Basta acessar o arquivo de configurações do vscode e colar o trecho:

```js
 "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    "editor.formatOnPaste": true,
```

---

## Aliases Git:

Acessar arquivo `.gitconfig`

Colar o código:

```yaml
[user]
  email = email@email.com
  name = Nome

[alias]
  ci = commit
  co = checkout
  cm = checkout master
  cb = checkout -b
  s = status -sb
  sf = show --name-only
  l = log --pretty=format:'%Cred%h%Creset %C(bold)%cr%Creset %Cgreen<%an>%Creset %s' --max-count=30
  incoming = !(git fetch --quiet && git log --pretty=format:'%C(yellow)%h %C(white)- %C(red)%an %C(white)- %C(cyan)%d%Creset %s %C(white)- %ar%Creset' ..@{u})
  outgoing = !(git fetch --quiet && git log --pretty=format:'%C(yellow)%h %C(white)- %C(red)%an %C(white)- %C(cyan)%d%Creset %s %C(white)- %ar%Creset' @{u}..)
  unstage = reset HEAD --
  undo = checkout --
  rollback = reset --soft HEAD~1
```

---

## Aliases .zshrc:

Você pode adicionar atalhos no .zshrc, que facilitam bastante na rotina de desenvolvimento, você pode incluir coisas como setup de arquivos, alterações de ambientes, dentro outras coisas.