---
title: Dicas de Styled Component
author: fziliotti
date: 2023-02-21 04:33:00 +0800
categorias: ["React, Styled"]
tags: [seo, web]
---
# Introdução

Styled-components é uma biblioteca Javascript responsável por permitir o uso de CSS dentro do Javascript. Isso facilita a criação de componentes inteligentes sem a necessidade de criação de muitas classes. Além disso, ele facilita a integração e interação entre Apps Web e Mobile, por conta do funcionamento para React e React-Native.

Existem vários outros benefícios e motivaçÕes que podem ser lidos na [documentação oficial da biblioteca.]([https://](https://styled-components.com/docs/basics#motivation))

# Criação de Temas

Você pode criar a estrutura de pastas: `src/styles/themes`. Dentro da pasta themes, pode criar o arquivo `default.ts` contendo o seguinte conteúdo:

```ts
export const defaultTheme = {
  white: "#FFF",

  "gray-100": "#E1E1E6",
  "gray-300": "#C4C4CC",

  "green-300": "#00B37E",
  "green-500": "#00875F",

  "red-500": "#AB222E",
  "red-700": "#7A1921",

  "yellow-500": "#FBA94C",
};
```

Após isso, em sua aplicação, você precisa usar o Provider do Styled Components que fornecerá os dados dos temas para os componentes da aplicação.

```jsx
export function App() {
  return (
    <ThemeProvider theme={defaultTheme}>
      <BrowserRouter>
        <Router />
      </BrowserRouter>
    </ThemeProvider>
  );
}
```

> Se você quiser criar outros temas, bastaria criar novos arquivos de temas, semelhante ao `default.ts`, e de acordo com alguma interação do usuário, alterar o estado e variável que será passada para o `<ThemeProvider />` acima.

Dicas para typescript: Para que o Typescript interprete e entenda corretamente o Theme de sua aplicação será necessário sobrescrever a tipagem padrão, um exemplo pode ser:

```ts
import "styled-components";
import { defaultTheme } from "../styles/themes/default";

type ThemeType = typeof defaultTheme;

declare module "styled-components" {
  export interface DefaultTheme extends ThemeType {}
}
```

# Estilos Globais com StyledComponents

Na estrutura criada para os temas, você pode adicionar um arquivo `src/styles/global.ts` para conter o código dos estilos globais da aplicação.

```js
import { createGlobalStyle } from "styled-components";

export const GlobalStyle = createGlobalStyle`
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  :focus {
    outline: none;
    box-shadow: 0 0 0 2px ${(props) => props.theme["green-500"]};
  }

  body {
    background: ${(props) => props.theme["gray-900"]};
    color: ${(props) => props.theme["gray-300"]};
    -webkit-font-smoothing: antialiased;
  }

  body, input, textarea, button {
    font-family: 'Roboto', sans-serif;
    font-weight: 400;
    font-size: 1rem;
  }
`;
```
# Considerações

Nos exemplos, utilizei Typescript, mas eles podem ser facilmente replicáveis para aplicações que fazem uso do javascript (ES6+)

Existem outras formas de utilizar o CSS-in-JS como as bibliotecas [Emotion](https://emotion.sh/docs/introduction), [Stitches](https://stitches.dev/). Mas Styled-Components se mantém bastante popular e com uma comunidade bastante ativa. Sendo minha principal opção no momento.