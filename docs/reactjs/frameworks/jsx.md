---
id: jsx
Titule: 1. JSX
description: ¿Qué es JSX? ¿Qué relación existe entre JSX y React?
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

# 1. JSX

Cada componente de **React** es una función de **JavaScript** que puede contener algo de marcado que **React** renderiza en el navegador. Los componentes de **React** utilizan una sintaxis extendida que se llama **JSX** para representar ese marcado. **JSX** se parece muchísimo a **HTML**, pero es un poco más estricto y puede mostrar información dinámica.

:::tip
**JSX** es una extensión de sintaxis para **JavaScript** que permite escribir marcado similar a **HTML** dentro de una archivo **JavaScript**
:::

A continuación tenemos el archivo **Componente.jsx** que define y exporta el componente **Componente**. El retorno de este componente es vacío. Es decir, aún cuando puede exportar un elemento **HTML**, por el momento, el componente no retorna ningún elemento. 

```javascript title="/src/Componente.jsx"
export const Componente = () => {
    return(
        <></>
    )
}
```

Al modificar el archivo **Componente.jsx** y el componente **Componente** retornamos ahora dos elementos **HTML**. El primer elemento es un parráfo y el segundo elemento es un título. 


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
**JSX** permite escribir marcas similares a **HTML** dentro de un archivo **JavaScript**, manteniendo la lógica de renderizado y el contenido en el mismo lugar. A veces vas a querer agregar un poco de lógica JavaScript o hacer referencia a una propiedad dinámica dentro de ese marcado
:::

Al modificar nuevamente el archivo **Componente.jsx** y el componente **Componente** retornamos ahora dos elementos **HTML**. El primer elemento es un parráfo y el segundo elemento es un título. Sin embargo, en el elemento parráfo se dinamiza el valor que debe mostrarse según el valor de la variable **nombre**. 

```javascript title="/src/Componente.jsx"
export const Componente = () => {
    const nombre = "Componente"
    return(
        <>
         <p>Hola, soy un {nombre}</p>
         <h2>Y soy un título</h2>
        </>
    )
}
```

## Fragmentos 

:::tip
Envuelve elementos en un **Fragment** para agruparlos en situaciones donde necesites un solo elemento. Agrupar elementos en **Fragment** no tiene efecto en el **DOM** resultante; ya que quedará igual que si los elementos no estuvieran agrupados. 

Para poder hacer uso del elemento **Fragment** debemos importarlo al inicio de todo

```javascript
import { Fragment } from 'react'
```

:::

A continuación creamos el archivo **Fragment.jsx** el cuál exporta el componente **FragmentApp**. El componente **FragmentApp** retorna un elemento **Fragment** que a su vez encapsula un parráfo.  

```javascript title="/src/Fragment.jsx"
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
