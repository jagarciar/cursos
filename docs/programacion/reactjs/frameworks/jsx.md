---
id: jsx
Titule: JSX
description: En este tutorial vamos a entender la sintaxis extendida llamada JSX usada en ReactJS
author: jeogarod
sidebar_position: 1
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - jsx
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# JSX

Cada componente de **React** es una función de **JavaScript** que puede contener algo de marcado que **React** renderiza en el navegador. Los componentes de **React** utilizan una sintaxis extendida que se llama **JSX** para representar ese marcado. **JSX** se parece muchísimo a **HTML**, pero es un poco más estricto y puede mostrar información dinámica.

:::tip
**JSX** es una extensión de sintaxis para **JavaScript** que permite escribir marcado similar a **HTML** dentro de una archivo **JavaScript**
:::

A continuación tenemos el archivo **Componente.jsx** que define y exporta el componente **Componente**. El componente retorna en un **Fragmento <>....</>** un parráfo y un sub-título. 

```javascript title="/src/Componente.jsx"
export const Componente = () => {
    return(
        <>
         <p>Hola, soy un componente</p>
         <h2>Y soy un título</h2>
        </>
    )
}
```

:::tip
**JSX** permite escribir marcas similares a **HTML** dentro de un archivo **JavaScript**, manteniendo la lógica de renderizado y el contenido en el mismo lugar.
:::

## Fragmentos 

:::tip
JSX envuelve elementos en un **Fragment** para agruparlos en situaciones donde necesites un solo elemento. Agrupar elementos en **Fragment** no tiene efecto en el **DOM** resultante; ya que quedará igual que si los elementos no estuvieran agrupados. 

Para poder hacer uso del elemento **Fragment** debemos importarlo al inicio de todo

```javascript
import { Fragment } from 'react'
```
:::

A continuación creamos el archivo **FragmentApp.jsx** el cuál exporta el componente **FragmentApp**. El componente **FragmentApp** retorna un elemento **Fragment** que a su vez encapsula un parráfo.  

```javascript title="/src/FragmentApp.jsx"
import React from 'react'
import { Fragment } from 'react'

export const FragmentApp = () => {
  return (
    <Fragment>
        <p>Hola soy un componente</p>
    </Fragment>
  )
}
```
