---
id: useEffect
title: 11. useEffect
sidebar_position: 11
author: jeogarod
description: ¿Qué es useEffect? ¿Cómo aporta en un componente funcional?
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - useEffect
  - hooks
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 11. useEffect

El **useEffect** en React es un tipo de hook que se incorporó en la versión de React 16.8. Como su nombre lo indica, este hook nos permite definir efectos. Los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente. **useEffect** recibe como parámetro una función que se ejecutará cada vez que nuestro componente se renderice, ya sea por un **cambio de estado**, por **recibir props nuevas** o, y esto es importante, porque es la **primera vez que se monta**.

:::tip
Con el hook **useEffect** en React, también podemos ejecutar trozos en las otras fases del ciclo de vida, ya sea en **updating** o en **unmounting**. En este orden de ideas, el hook **useEffect** en React equivale a una combinación de las funciones **componentDidMount**, **componentDidUpdate** y **componentWillUnmount**.

Para poder usarlo debes importarlo al inicio de nuestro Componente. 

```javascript
import React, { useEffect } from 'react'
```
:::

:::tip
Otro caso de uso muy típico de **useEffect** es la suscripción a los eventos del DOM. Por ejemplo, puede ser útil para subscribirnos al evento de scroll, o el de Intersection Observer para crear fácilmente un componente que sirva de Lazy Load… o simplemente para escuchar el evento resize del window
:::

## Loops en la renderización 

Por defecto los efectos se disparan cada vez que se realiza un nuevo renderizado pero podemos evitar que el efecto se vuelva a ejecutar pasándole un segundo parámetro al hook. El parámetro es un array con todos los valores de los que depende nuestro efecto, de forma que sólo se ejecutará cuando ese valor cambie.


