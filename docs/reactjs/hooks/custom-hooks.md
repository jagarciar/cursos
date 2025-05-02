---
id: custom-hooks
title: 7. Custom hooks
sidebar_position: 7
author: jeogarod
description: ¿Qué son los custom hooks? ¿En qué se diferencian con los hooks?
tags:
  - react
  - reactjs
  - npm
  - vite
  - useState
  - useEffect
  - useFetch
  - hooks
  - useForm
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 7. Custom hooks

Un **Custom Hook** es una **función JavaScript** que utiliza otros **Hooks** de React para encapsular lógica de manera que pueda ser reutilizada en varios componentes. Estos hooks no son más que una extensión de los hooks estándar de React, como useRef, [useState](/docs/reactjs/hooks/useState.md) o [useEffect](/docs/reactjs/hooks/useEffect.md), permitiéndonos crear nuestra propia lógica que puede ser compartida y reutilizada en varios componentes. Es como un contenedor para la lógica de estado y efectos, permitiendo su reuso sin duplicar código.

:::tip
La **gestión de estados** es uno de los casos de uso más comunes para los **custom hooks** en React. Estos permiten crear **manejadores de estado** que son reutilizables entre diferentes componentes. Por ejemplo, un custom hook podría manejar la lógica de un formulario, almacenando y actualizando valores de los campos de manera eficiente. Esto resulta en un código más limpio y modular, facilitando la mantenibilidad y escalabilidad de las aplicaciones.
:::

:::info
Los **custom hooks** pueden encapsular la lógica para realizar peticiones **HTTP**, manejar respuestas y errores, y gestionar estados de carga. Esto simplifica enormemente los componentes que consumen datos de **APIs**, ya que toda la lógica de red y manejo de datos se abstrae en un hook reutilizable. 
:::

Para crear un **custom hook** en **React**, comenzamos definiendo una función que encapsula la lógica o estado que deseamos reutilizar. Es importante recordar que todos los **hooks** personalizados deben comenzar con **use**, por ejemplo, **useFetch**.

:::info
Un ejemplo práctico podría ser un **hook** de estado que gestione un variable de estado. Este hook utilizaría **useState** para almacenar y actualizar el valor del variable. Cada vez que necesitemos usar esta variable en nuestros componentes, podríamos usar nuestro **custom hook** para manejar esta lógica de manera eficiente y reutilizable.
:::



## useFetch





## useLocalStorage


