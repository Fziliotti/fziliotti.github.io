---
title: "Composition Pattern: Exemplo prático no React"
author: fziliotti
date: 2024-03-14 04:33:10 +0800
categories: ["Desenvolvimento"]
tags: [frontend]
---

## Introdução

O padrão de composição (Composition Pattern) é um conceito comum na programação orientada a objetos, onde objetos são compostos de outros objetos para obter funcionalidades mais complexas. No contexto do desenvolvimento frontend com React, o padrão de composição é frequentemente utilizado para criar componentes reutilizáveis e modularizados.


## Exemplo Simples

Vamos criar um exemplo simples para demonstrar o padrão de composição em React:

Suponha que queremos criar um componente Card que pode exibir diferentes tipos de conteúdo, como título, texto e uma imagem. Em vez de criar um componente enorme que abrange todas essas funcionalidades, podemos usar o padrão de composição para criar componentes menores e mais especializados e, em seguida, combiná-los para formar o Card.

```jsx
import React from 'react';

// Componente reutilizável para o título
const Title = ({ children }) => <h2>{children}</h2>;

// Componente reutilizável para o texto
const Text = ({ children }) => <p>{children}</p>;

// Componente reutilizável para a imagem
const Image = ({ src, alt }) => <img src={src} alt={alt} style={{ maxWidth: '100%' }} />;

// Componente Card que utiliza os componentes acima por composição
const Card = ({ title, text, imageSrc, imageAlt }) => (
  <div className="card">
    <Title>{title}</Title>
    <Text>{text}</Text>
    <Image src={imageSrc} alt={imageAlt} />
  </div>
);

// Exemplo de uso do componente Card
const App = () => {
  return (
    <div>
      <Card
        title="Título do Card"
        text="Este é um exemplo de texto dentro do Card."
        imageSrc="https://via.placeholder.com/150"
        imageAlt="Imagem de exemplo"
      />
    </div>
  );
};

export default App;

```

## Exemplo um pouco mais complexo


```jsx
interface CustomButtonProps extends React.ComponentProps<'button'> {
  variant?: 'primary' | 'secondary';
  size?: 'small' | 'large';
}

export const CustomButton: React.FC<CustomButtonProps> = ({
  variant = 'primary',
  size = 'medium',
  className,
  children,
  ...props
}) => {
  const classes = `btn ${variant} ${size} ${className}`;

  return (
    <button className={classes} {...props}>
      {children}
    </button>
  );
};

export const CustomIcon: React.FC<React.ComponentProps<typeof Icon>> = (props) => {
  return <Icon {...props} />;
};

export const CustomText: React.FC<React.ComponentProps<'span'>> = ({
  children,
  ...props
}) => {
  return <span {...props}>{children}</span>;
};

export const CustomCta = {
  Button: CustomButton,
  Icon: CustomIcon,
  Text: CustomText,
};

```

E com o componente criado, você poderá criar diferentes tipos de botões, como o botão de Like:

```jsx
import React from 'react';
import { CustomCta } from './components/CustomCta'; 

const CtaButtonWithIcon = () => {
  return (
    <CustomCta.Button variant="secondary" onClick={() => alert('Botão Clicado')}>
      <CustomCta.Icon icon="heart" />
      <CustomCta.Text>Like</CustomCta.Text>
    </CustomCta.Button>
  );
};

export default CtaButtonWithIcon;
```

Botão favorito:

```jsx
import React from 'react';
import { CustomCta } from './components/CustomCta'; 

const CustomizedCtaButton = () => {
  return (
    <CustomCta.Button variant="primary" onClick={() => alert('Botão Clicado')}>
      <CustomCta.Icon icon="star" />
      <CustomCta.Text>Favorito</CustomCta.Text>
    </CustomCta.Button>
  );
};

export default CustomizedCtaButton;
```

Sem o padrão de Composition, o mesmo componente poderia ser criado da seguinte forma:

```jsx
import React from 'react';

const CustomCta = ({ variant = 'primary', onClick, icon, text }) => {
  let iconElement = null;
  if (icon) {
    iconElement = <span className={`icon icon-${icon}`} />;
  }

  return (
    <button className={`btn ${variant}`} onClick={onClick}>
      {iconElement}
      {text}
    </button>
  );
};

export default ButtonWithIconAndText;
```

Apesar de que nesse exemplo a forma sem o pattern Composition fique bem fácil de entender, a ideia é refletir uma outra forma de criar componentes que são mais fáceis de estender ou modificar. Possivelmente se o componente de CustomCta evoluísse, muitas props seriam passadas para ele, dificultando a manutenção.


### Conclusão

A escolha entre usar o composition pattern e criar um componente de botão sem o composition pattern depende das necessidades específicas do seu projeto, do seu estilo de codificação e das preferências da sua equipe. Vamos considerar algumas vantagens e desvantagens de cada abordagem:

#### Composition Pattern:

**Vantagens:**
- Modularidade: Permite criar componentes mais modulares e reutilizáveis, facilitando a construção e a manutenção de interfaces complexas.
- Flexibilidade: Componentes individuais podem ser combinados de várias maneiras para criar uma variedade de interfaces.
- Separação de Responsabilidades: Cada componente tem uma única responsabilidade, facilitando a compreensão e a manutenção do código.

**Desvantagens:**
- Complexidade Adicional: Pode exigir um pouco mais de trabalho para criar e gerenciar vários componentes em comparação com uma abordagem menos modular.
- Overhead de Abstração: Em alguns casos, a criação de muitos componentes pequenos pode levar a um aumento na complexidade e no overhead de abstração.


#### Sem Composition Pattern:

**Vantagens:**
- Simplicidade: Pode ser mais simples e direto criar componentes sem dividir a funcionalidade em partes menores.
- Menos Overhead: Menos abstrações e componentes podem levar a menos overhead de gerenciamento.

**Desvantagens:**
- Menos Modularidade: Componentes podem ser menos modulares e reutilizáveis, tornando mais difícil a manutenção de interfaces complexas.

- Dificuldade em Extensão: Pode ser mais difícil estender ou modificar componentes sem quebrar outras partes do código.

Em geral, o **composition pattern** é amplamente preferido na comunidade React devido à sua capacidade de criar componentes mais flexíveis e modulares. No entanto, a abordagem **sem composition pattern** pode ser adequada em casos simples ou em projetos onde a simplicidade é mais valorizada do que a flexibilidade e a reutilização.