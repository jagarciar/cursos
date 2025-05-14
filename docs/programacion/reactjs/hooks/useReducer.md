---
id: useReducer
title: useReducer
sidebar_position: 7
author: jeogarod
description: En este tutorial vamos hacer uso del hook useReducer para definir un estado global de un proyecto ReactJS y manipularlo a través de reductores.
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - hooks
  - useReducer
  - useEffect
  - reducer
  - useState
  - estado
last_update:
  date: 05/02/2025
  author: Jeyson Andrés García Rodríguez
---

# useReducer

Es una función que especifica cómo el **estado de una aplicación** debe cambiar en respuesta a una acción enviada a través de un **dispatch**. Un **reducer** toma el **estado actual** y una **acción** como **argumentos** y **devuelve** un **nuevo estado** que refleja como debería cambiar el estado de la aplicación en respuesta a esa acción específica. 

:::tip
Aunque no es necesario usar **useReducer** para gestionar el estado en **React**, puede ser útil en situaciones donde el **estado** y las **transiciones** de **estado** son más complejadas o donde se necesita manejar lógica más avanzada que [**useState**](/docs/programacion/reactjs/hooks/useState.md) no puede cubrir facilmente.
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

:::tip
El nombre de **useReducer** da pie a confundirlo con [**Redux**](/docs/programacion/reactjs/frameworks/redux.md), pero en realidad son cosas completamente diferentes.

**useReducer** es un **hook** de **React** para **actualizar** un **estado** interno por medio de una función llamada **reducer**. [**Redux**](/docs/programacion/reactjs/frameworks/redux.md) es una **arquitectura** que nos permite **abstraer** el manejo de un **estado** global en una aplicación.
:::

Supongamos el siguiente ejemplo:

Vamos a modelar el **estado** de nuestra aplicación como un arreglo o lista de elementos donde cada elemento representa una tarea. Cada tarea tiene un identificador, un nombre, una bandera que determina si la tarea ya fue finalizada o no y una bandera que determina si la tarea fue buscada o no. 

```javascript
const initialState = [
    {
        id:0,
        name:"Hacer commit en la base de datos",
        isCompleted:false,
        isSelected:false
    }
]
```

Nuestra función **reducer** recibirá el **estado** y la **acción**. Dentro de las acciones que disponemos en nuestra aplicación se encuentra **ADD** y **FIND**. La acción **ADD** adicionará un elemento a nuestro arreglo o lista de tareas. La acción **FIND** consultará un elemento en el arreglo o lista de tareas. 

- La función **ADD** actualizará el valor del campo **isSelected** para todos los elementos del arreglo o lista a **false**. 
- La función **FIND** actualizará el valor del campo **isSelected** a **true** para el elemento del arreglo o lista que fue encontrado. 

```javascript
const reducer = (state, action) => {
    const { name } = action.payload;
    switch (action.type) {
        case 'ADD':
            state.map((x) => {
                x.isSelected = false;
            })
            return [
                ...state,
                {
                    id: uuidv4(),
                    name: name,
                    isSelected : false,
                    isCompleted: false
                }
            ]
        case 'FIND':
            state.map((x) => {
                if (x.name == name) {
                    x.isSelected = true;
                }
            })
            return state;
        default:
            return state;
    }
}
```

El componente **ComponenteApp** tiene dos variables de estado : **tarea** y **tareaEncontrada** con sus respectivas funciones **set** **setTarea** y **setTareaEncontrada**. **ComponenteApp** importa un **reducer** con un **estado inicial** definidos previamente. **ComponenteApp** implementó tres funciones : **handleChange**, **addTarea** y **buscarTarea**.  La función **handleChange** actualizará el valor de la variable de estado **tarea**. La función **addTarea** invocará el **dispatch** enviando el **type = 'ADD'** y el nombre de la tarea. La función **buscarTarea** invocará el **dispatch** enviando el **type = 'FIND'** y el nombre de la tarea. Adicionalmente, el componente **ComponenteApp** definió el **hook** **useEffect** para que cada que se actualice el valor de la variable de estado **tarea** consulte del **estado** del **hook** **useReducer** si algún elemento del arreglo o lista de tareas fue buscada o no. El **hook** **useEffect** actualiza el valor de la variable de estado **tareaEncontrada**. 

A tener en cuenta sobre las funciones del componente:

- La función **addTarea** actualiza el valor de la variable de estado **tareaEncontrada** dejandola en nulo o vacío. 
- Tanto para la función **addTarea** como para la función **buscarTarea** el objeto **action** contiene un atributo **type** (con dos posibles valores : **ADD** o **FIND**) y un atributo **payload**. El atributo **payload** contiene únicamente el campo **name**, el cuál representa el nombre de la tarea. 
- Tanto la función **addTarea** como la función **buscarTarea** actualizan el valor de la variable de estado **tarea**. 

A tener en cuenta sobre el retorno del componente:

- El componente **ComponenteApp** retorna una caja de texto donde el usuario podrá digitar el nombre de la tarea. Esta caja de texto dispara la función **handleChange** a partir del evento **onChange**. 
- El componente **ComponenteApp** retorna dos botones : el primer botón dispara la función **addTarea** y el segundo botón dispara la función **buscarTarea**. Ambos botones disparan las funciones a partir del evento **onClick**. 
- El componente **ComponenteApp** retorna una **lista desordenada** donde cada elemento es una tarea. Cada tarea tiene su identificador, un nombre, una bandera que determina si está completada o no y una bandera que determina si fue buscada o no. 
- El componente **ComponenteApp** retorna una **lista desordenada** de un único elemento siempre que el valor de la variable de estado **tareaEncontrada** es diferente de nulo o vacío. 
- El componente **ComponenteApp** retorna una **lista desordenada** de varios elementos siempre que el valor de la variable de estado **tareaEncontrada** sea nulo o vacío. 

```javascript
import React, { useEffect } from 'react'
import { useReducer, useState } from 'react';

export const ComponenteApp = () => {

    const [tareaEncontrada, setTareaEncontrada] = useState(null);
    const [tarea, setTarea] = useState('');
    const [state, dispatch] = useReducer(reducer, initialState);

    const handleChange = (event) => {
        setTarea(event.target.value);
    }

    const addTarea = (event) => {
        const action = {
            type: 'ADD',
            payload: {
                name: tarea
            }
        }
        dispatch(action);
        setTarea('');
        setTareaEncontrada(null);
    }

    const buscarTarea = (event) => {
        const action = {
            type: 'FIND',
            payload: {
                name: tarea
            }
        }
        dispatch(action);
        setTarea('');
    }

    useEffect(() => {
        let encontrada = false;
        state.map((item) => {
            if(item.isSelected){
                encontrada = true;
                setTareaEncontrada(item);
            }
        })
        if(!encontrada){
            setTareaEncontrada(null);
        }
    },[tarea])

    return (
        <>


            <input id="tarea" name="tarea" type="text" onChange={handleChange} value={tarea} />
            <button onClick={() => addTarea()}>Adicionar</button>
            <button onClick={() => buscarTarea()}>Buscar</button>

            <ul>
                {
                    tareaEncontrada == null && state && state.map((item) => {
                        return (<li key={item.id} value={item.name}>{item.name}</li>)
                    })
                }
            </ul>
            <ul>
                {
                    tareaEncontrada != null && <li key={tareaEncontrada.id} value={tareaEncontrada.name}>{tareaEncontrada.name}</li>
                }
            </ul>
        </>
    )
}
```