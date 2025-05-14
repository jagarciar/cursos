---
id: intro-hooks
Titule: 1. Introducción
sidebar_position: 1
description: En React los hooks permiten administrar el estado y otras funciones sin tener que escribir una clase.
author: jeogarod
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - useState
  - useEffect
  - useRef
  - useMemo
  - useCallback
  - useForm
  - useCounter
  - useReducer
  - hooks
  - ciclo-vida
  - montaje
  - desmontaje
  - renderizado
  - estado
  - componente-funcional
last_update:
  date: 05/02/2025
  author: Jeyson Andrés García Rodríguez
---

# 1. Introducción

En el mundo de la programación, los **hooks** son una herramienta clave para interactuar con el **ciclo de vida** de las aplicaciones de manera más flexible y eficiente. Estos elementos permiten la integración de funcionalidades adicionales sin modificar el código base, y promueven una mayor personalización y reutilización de componentes. 

La principal ventaja de los **Hooks** es que permiten una manera más clara y sencilla de trabajar con el **estado** de los **componentes**. Los [**componentes de clase**](/docs/programacion/reactjs/proyecto/componente-clase.md) necesitan definir un constructor y el estado en el mismo, agregando complejidad al código y haciendo que sea más difícil de entender. Los [**componentes funcionales**](/docs/programacion/reactjs/proyecto/componente-funcional.md) con Hooks permiten definir el estado de una manera más sencilla y legible.

:::tip
Hasta la versión **16.7** de **React**, solo era posible acceder a algunas funcionalidades a través de clases (como, por ejemplo, el **lifecycle**). Apesar de la posibilidad de crear componentes a partir de funciones, hasta esta versión solo recibían propiedades y no podían acceder a todas las funcionalidades de React, como lo hacían con las clases.

En la versión **16.8** de **React** se lanzaron **hooks**, que permiten utilizar varios recursos de forma sencilla a través de **funciones**. También ayuda a organizar la lógica utilizada dentro de los componentes.
:::

Existen dos tipos de **Hooks** en **React**, los **hooks del framework** que vienen predefinidos y los **hooks personalizados**, que cada desarrollador puede crear para poder reciclar funcionalidad entre componentes.

Dentro de los **hooks del framework** se encuentran:

1. [useState](/docs/programacion/reactjs/hooks/useState.md) 
2. [useEffect](/docs/programacion/reactjs/hooks/useEffect.md)
3. [useRef](/docs/programacion/reactjs/hooks/useRef.md) 
4. [useMemo](/docs/programacion/reactjs/hooks/useMemo.md) 
5. [useCallback](/docs/programacion/reactjs/hooks/useCallback.md) 
6. [useReducer](/docs/programacion/reactjs/hooks/useReducer.md) 
7. [useForm](/docs/programacion/reactjs/hooks/useForm.md) 
8. [useCounter](/docs/programacion/reactjs/hooks/useCounter.md) 
9. [useFetch](/docs/programacion/reactjs/hooks/useFetch.md) 
10. [useLocalStorage](/docs/programacion/reactjs/hooks/useLocalStorage.md)

:::warning
Los **hooks**, aunque increíbles, vienen con sus propios limitantes. Por un lado, sólo puedes mandarlos a llamar en el **cuerpo de la función**, y no pueden llamarse dentro de **condicionales**, **ciclos**, o cualquier otra estructura que agregue un nuevo nivel de ejecución al componente
:::