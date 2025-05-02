---
id: useReducer
title: 6. useReducer
sidebar_position: 6
author: jeogarod
description: ¿Qué es useReducer? ¿Qué es un reducer?
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - hooks
  - useReducer
  - reducer
  - useState
  - estado
last_update:
  date: 05/02/2025
  author: Jeyson Andrés García Rodríguez
---

# 6. useReducer

Es una función que especifica cómo el **estado de una aplicación** debe cambiar en respuesta a una acción enviada a través de un **dispatch**. Un **reducer** toma el **estado actual** y una **acción** como **argumentos** y **devuelve** un **nuevo estado** que refleja como debería cambiar el estado de la aplicación en respuesta a esa acción específica. 

:::tip
Aunque no es necesario usar **useReducer** para gestionar el estado en **React**, puede ser útil en situaciones donde el **estado** y las **transiciones** de **estado** son más complejadas o donde se necesita manejar lógica más avanzada que [**useState**](/docs/reactjs/hooks/useState.md) no puede cubrir facilmente.
:::

El **hook** **useReducer** está compuesto de un **estado inicial** y un **reducer** explicados a continuación:

**initialState** es el **estado inicial** de un componente.

```javascript
const initialState = {
    counter : 0
}
```

**reducer** es una función qué especifica como el **estado** debe cambiar en respuesta a las acciones. 

```javascript
const reducer = (state, action) => {
    switch(action.type){
        case 'INCREMENT':
            return { counter : state.counter + 1};
        case 'DECREMENT':
            return { counter : state.counter - 1};
        default:
            return state;
    }
}
```

El componente **ComponenteApp** importa a **useReducer**. El **hook** **useReducer** inicializa el **estado** del componente y proporciona una función **dispatch** que se utiliza para enviar **acciones** al **reducer**. **ComponenteApp** retorna en un parráfo el valor de la variable de estado **counter** y dos botones. El primer botón llama al **dispatch** con el argumento **type = 'INCREMENT'**. El segundo botón llama al **dispatch** con el argumento **type = 'DECREMENT'**. Es decir, al darle click al primer botón, el valor de la variable de estado **counter** se incrementa en 1 y al darle click al segundo botón, el valor de la variable de estado **counter** se decrementa en 1. 

```javascript
import React from 'react'
import { useReducer } from 'react';

export const ComponenteApp = () => {
  
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
        <p>Contador : {state.counter}</p>
        <button onClick={() => dispatch({type : 'INCREMENT'})}>Incrementar</button>
        <button onClick={() => dispatch({type : 'DECREMENT'})}>Decrementar</button>
    </>
  )
}
```