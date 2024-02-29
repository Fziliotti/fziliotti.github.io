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

## Uso de Generics no React

Se você estiver criando componentes que precisam ser flexíveis o suficiente para lidar com diferentes tipos de dados, os generics podem ser úteis .

```js
interface ListItem {
    id: number;
    text: string;
}

interface ListProps<T> {
    data: T[];
    renderItem: (item: T) => React.ReactNode;
}

function List<T>({ data, renderItem }: ListProps<T>) {
    return (
        <ul>
            {data.map(item => (
                <li key={item.id}>{renderItem(item)}</li>
            ))}
        </ul>
    );
}

// Uso do componente List
const items: ListItem[] = [
    { id: 1, text: "Item 1" },
    { id: 2, text: "Item 2" },
    { id: 3, text: "Item 3" }
];

const renderItem = (item: ListItem) => <span>{item.text}</span>;

const MyListComponent = () => {
    return <List data={items} renderItem={renderItem} />;
};

```

Outra situação que pode acontecer é no uso de hooks personalizados, um exemplo:

```js
import { useState } from 'react';

function useLocalStorage<T>(key: string, initialValue: T): [T, (value: T) => void] {
    const [storedValue, setStoredValue] = useState<T>(() => {
        const item = localStorage.getItem(key);
        return item ? JSON.parse(item) : initialValue;
    });

    const setValue = (value: T) => {
        setStoredValue(value);
        localStorage.setItem(key, JSON.stringify(value));
    };

    return [storedValue, setValue];
}

// Uso do hook personalizado
const [name, setName] = useLocalStorage<string>('name', 'John');


```

# Referências para consultar e aprender mais

Documentação Oficial do TypeScript:

- [TypeScript Handbook](https://https://www.typescriptlang.org/docs/handbook/intro.html)
- [React TypeScript Cheatsheet](https://https://react-typescript-cheatsheet.netlify.app/)
