---
title: Formulários em React
author: fziliotti
date: 2023-02-22 04:33:00 +0800
categories: ["Desenvolvimento"]
tags: [frontend]
---

# Introdução

Em react e no desenvolvimento web em geral, os formulários são elementos fundamentais de qualquer tipo de aplicação ou página na web. Por isso pensei de registrar alguns conceitos e dicas de desenvolvimento com React.


## Controlled x Uncontrolled

Componentes controlados basicamente vão manter em tempo real as informações no estado do componente, ou basicamente, na memória do navegador. Na maioria dos casos essa forma é a recomendada para implementar os formulários.

Nos componentes não controlados, as informações preenchidas pelo usuários serão gerenciadas pelo DOM do browser.

Na forma Controlled, o desenvolvedor tem fácil acesso aos valores dos inputs e dados do formulário, e também maior flexibilidade para modificar a interface. Já na forma Uncontrolled, geralmente ela acaba sendo mais indicada para evitar problemas de performance como re-renders desnecessários que um formulário desenvolvido da maneira Controlled pode ocasionar.


## React-hook-form

Ultimamente em meus projetos, tenho utilizado a bibliteca [React Hook Form](https://react-hook-form.com/) para lidar com formulários. Ela facilita bastante no gerenciamento de formulários, além de ter integração com ferramentas de validação como yup, zod e joi. Isso é especialmente importante para facilitar a criação de regras que nem sempre são facilmente criadas com Regex, no atributo patterns do HTML, por exemplo.


Exemplo da própria documentação oficial:

```jsx
import React from 'react';
import { useForm } from 'react-hook-form';

export default function App() {
  const { register, handleSubmit, formState: { errors } } = useForm();
  const onSubmit = data => console.log(data);
  console.log(errors);
  
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input type="text" placeholder="First name" {...register("First name", {required: true, maxLength: 80})} />
      <input type="text" placeholder="Last name" {...register("Last name", {required: true, maxLength: 100})} />
      <input type="text" placeholder="Email" {...register("Email", {required: true, pattern: /^\S+@\S+$/i})} />
      <input type="tel" placeholder="Mobile number" {...register("Mobile number", {required: true, minLength: 6, maxLength: 12})} />
      <select {...register("Title", { required: true })}>
        <option value="Mr">Mr</option>
        <option value="Mrs">Mrs</option>
        <option value="Miss">Miss</option>
        <option value="Dr">Dr</option>
      </select>

      <input {...register("Developer", { required: true })} type="radio" value="Yes" />
      <input {...register("Developer", { required: true })} type="radio" value="No" />

      <input type="submit" />
    </form>
  );
}
```

Para aplicações React que utilizam Typescript, eu geralmente gosto de usar a dupla React Hook Form com Zod. Um exemplo de formulário que faz uso dessas bibiliotecas e que peguei de um dos repositórios da rocketseat que achei legal:


```jsx
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import * as zod from 'zod'

const newCycleFormValidationSchema = zod.object({
  task: zod.string().min(1, 'Informe a tarefa'),
  minutesAmount: zod
    .number()
    .min(5, 'O ciclo precisa ser de no mínimo 5 minutos.')
    .max(60, 'O ciclo precisa ser de no máximo 60 minutos.'),
})

type NewCycleFormData = zod.infer<typeof newCycleFormValidationSchema>

export function Home() {
  const { register, handleSubmit, watch } = useForm<NewCycleFormData>({
    resolver: zodResolver(newCycleFormValidationSchema),
    defaultValues: {
      task: '',
      minutesAmount: 0,
    },
  })

  function handleCreateNewCycle(data: NewCycleFormData) {
    console.log(data)
  }

  const task = watch('task')
  const isSubmitDisable = !task

  return (
    <HomeContainer>
      <form onSubmit={handleSubmit(handleCreateNewCycle)}>
        <FormContainer>
          <label htmlFor="task">Vou trabalhar em</label>
          <TaskInput
            id="task"
            list="task-suggestions"
            placeholder="Dê um nome para o seu projeto"
            {...register('task')}
          />

          <datalist id="task-suggestions">
            <option value="Projeto 1" />
            <option value="Projeto 2" />
            <option value="Projeto 3" />
            <option value="Banana" />
          </datalist>

          <label htmlFor="minutesAmount">durante</label>
          <MinutesAmountInput
            type="number"
            id="minutesAmount"
            placeholder="00"
            step={5}
            min={5}
            max={60}
            {...register('minutesAmount', { valueAsNumber: true })}
          />

          <span>minutos.</span>
        </FormContainer>

        <StartCountdownButton disabled={isSubmitDisable} type="submit">
          Começar
        </StartCountdownButton>
      </form>
    </HomeContainer>
  )
}
```


## Conclusão

Formulários desenvolvidos na forma Controlled geralmente são indicados para formulários com poucos elementos e inputs, como logins, inscriçÕes de e-mail em newsletter e outros casos pontuais.

Para formulários mais complexos e com muitos inputs, para evitar problemas de performance, uma abordagem interessante pode ser a forma Uncontrolled.

Bibliotecas como Formik e react-hook-form auxiliam bastante na construção de formulários robustos, com validações de inputs.