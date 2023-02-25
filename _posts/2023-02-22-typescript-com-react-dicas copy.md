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


