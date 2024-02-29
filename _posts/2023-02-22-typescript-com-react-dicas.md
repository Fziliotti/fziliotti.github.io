---
title: Dicas de Typescript com React
author: fziliotti
date: 2023-02-22 04:33:00 +0800
categorias: ["Dev", "Setup"]
tags: [setup, configs]
---

# Componente React que herda atributos de elemento HTML

Exemplo de componente de Avatar no React que herda atributos e tipagem do elemento img do HTML.

```jsx
import { ImgHTMLAttributes } from "react";
import styles from './Avatar.module.css'

// interface que extende os atributos do elemento img HTML
interface AvatarProps extends ImgHTMLAttributes<HTMLImageElement> {
  hasBorder?: boolean;
}


// Uso de rest operator
export function Avatar({ hasBorder = true, ...props}: AvatarProps) {
  return (
    <img
      className={hasBorder ? styles.avatarWithBorder : styles.avatar}
      {...props}
    />
  );
}
```


## Integração com APIs

```js
interface UserData {
    id: number;
    name: string;
    email: string;
}

const fetchUserData = async (): Promise<UserData> => {
    const response = await axios.get<UserData>('https://api.example.com/user');
    return response.data;
};
```


## Trabalhando com Eventos

```js
const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {
    console.log('Button clicked');
};
```

# Referências para consultar e aprender mais

Documentação Oficial do TypeScript:

- [TypeScript Handbook]([https://](https://www.typescriptlang.org/docs/handbook/intro.html))
- [React TypeScript Cheatsheet]([https://](https://react-typescript-cheatsheet.netlify.app/))
