---
id: useSelector
title: useSelector
sidebar_position: 11
author: jeogarod
description: En este tutorial vamos hacer uso del hook useSelector para acceder al estado global de la aplicación en un proyecto ReactJS haciendo uso de Redux
tags:
  - react
  - reactjs
  - npm
  - vite
  - useSelector
  - redux
  - hooks
last_update:
  date: 05/14/2025
  author: Jeyson Andrés García Rodríguez
---

# useSelector

En el contexto de [**Redux**](/docs/programacion/reactjs/frameworks/redux.md), **useSelector** es una herramienta crucial que permite a los componentes de React acceder al **estado global** almacenado en el **store** de **Redux**. El hook **useSelector** es una función que recibe el **estado** y *devuelve un valor derivado* del **estado**. Esto facilita la obtención de datos específicos de la aplicación y su renderización en el componente.

:::tip
El **hook** **useSelector** se utiliza en **componentes funcionales** de **React** para seleccionar y acceder a partes específicas del **estado global** almacenado en el **almacén** de [**Redux**](/docs/programacion/reactjs/frameworks/redux.md). En lugar de acceder directamente al estado global utilizando **store.getState()**, **useSelector** proporciona una forma más conveniente de suscribirse a los cambios de estado y acceder a los datos que un componente necesita.
:::

Uno de los aspectos más interesantes de **useSelector** es su capacidad para optimizar el rendimiento de los componentes. Supongamos que tenemos un componente que solo necesita actualizarse cuando un **valor específico en el estado cambia**. En lugar de renderizar el componente cada vez que cambia cualquier parte del estado, puedes utilizar **useSelector** para seleccionar solo ese valor particular. Esto disminuye la frecuencia de renderizado innecesario y mejora la eficiencia general de la aplicación.

:::tip
El **hook** **useSelector** es similar a **mapStateToProps**. La única diferencia es que la función **mapStateToProps** recibe como argumentos múltiples valores mientras que el **hook** **useSelector** toma el **estado** como único argumento. 
:::