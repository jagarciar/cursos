---
id: componentes-funcional
title: 5. Componentes funcionales
sidebar_position: 4
author: jeogarod
description: Creación de un componente funcional.
tags:
    - react
    - reactjs
    - vite
    - npm
    - componente-funcional
    - export
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 4. Componentes funcionales

**React** es una biblioteca de **JavaScript** para renderizar **interfaces de usuario** (**UI** por sus siglas en inglés). La **UI** se construye a partir de pequeñas unidades como botones, texto e imágenes. **React** te permite combinarlas en **componentes reutilizables** y anidables. **React** clasifica los componentes en : **componentes funcionales** y **componentes de clase**.

Los **componentes funcionales** son **funciones** que reciben el objeto **props** y retornan un **ReactNode** (**ReactNode** puede representar cualquier elemento **HTML**, una variable, entre otras). 

A continuación tenemos en un archivo **Componente.jsx** la definición y creación de un componente nombrado **Componente**. Por el momento este componente no definirá ningún parámetro
pero retornará un elemento **HTML** (en este caso un parráfo).

```javascript title="/src/Componente.jsx"
import React from 'react'

export const Componente = () => {
    return(
        <p>Hola, soy un componente</p>
    )
}
```

:::tip
La palabra reservada **export** permite exponer este componente **Componente** para que pueda ser **reutilizado** en otro componente
:::