---
title: Redux toolkit - exemplo simples
author: fziliotti
date: 2024-02-29 04:33:00 +0800
categories: ["Dev", "Frontend"]
tags: [dev, frontend]
---

## Introdução
O gerenciamento de estado em aplicativos React pode se tornar complexo à medida que a aplicação cresce em tamanho e escopo. Redux, uma biblioteca popular para gerenciamento de estado, oferece uma solução robusta, mas a configuração inicial pode parecer um pouco verbosa.

Neste guia, exploraremos uma ferramenta que veio para simplificar drasticamente o uso do Redux: o Redux Toolkit. Essa biblioteca é uma adição oficial ao ecossistema Redux e foi projetada para tornar o desenvolvimento com Redux mais intuitivo, eficiente e livre de boilerplate.
 
## Exemplo prático e simples de entender

Arquivo `CounterSlice.js`:

```jsx
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { count: 0 },
  reducers: {
    increment: (state) => {
      state.count += 1;
    },
    decrement: (state) => {
      state.count -= 1;
    },
  },
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;
```

Arquivo `store.js` :

```jsx
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './counterSlice';

const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});

export default store;
```

Arquivo `Counter.js`:

```jsx
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement } from '../counterSlice';

const Counter = () => {
  const count = useSelector((state) => state.counter.count);
  const dispatch = useDispatch();

  return (
    <div>
      <h2>Contador: {count}</h2>
      <button onClick={() => dispatch(increment())}>Incrementar</button>
      <button onClick={() => dispatch(decrement())}>Decrementar</button>
    </div>
  );
};

export default Counter;
```

Arquivo `App.js`:

```jsx
import React from 'react';
import { Provider } from 'react-redux';
import store from './store';
import Counter from './components/Counter';

function App() {
  return (
    <Provider store={store}>
      <div className="App">
        <Counter />
      </div>
    </Provider>
  );
}

export default App;

```