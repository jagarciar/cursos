---
id: redux
Title: Redux
description: En este tutorial vamos aprender a usar Redux en un proyecto ReactJS haciendo uso de los hooks useSelector y useDispatch. 
sidebar_position: 3
author: jeogarod
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - redux
  - estado
  - flux
  - useState
  - useReducer
  - useSelector
  - useDispatch
last_update:
  date: 02/05/2025
  author: Jeyson Andrés García Rodríguez
---

# Redux

**Redux** es un contenedor de estado para aplicaciones JavaScript especialmente útil en el contexto de aplicaciones de **React**. Fue diseñado para gestionar el **estado** de la aplicación de una manera predecible y centralizada. 

:::tip
**Redux** es la implementación del **patrón de arquitectura de datos** [**flux**](/blog/2025-05-18-Flux.md) que permite manejar el **estado de la aplicación** de una manera predecible. Está pensado para reducir el número de relaciones entre componentes de la aplicación y mantener un flujo de datos sencillo.
:::

![Redux](/img/Redux.png)

**Redux** esta basado en:

1. El estado de toda tu aplicación esta almacenado en un árbol guardado en un único store.
2. La única forma de modificar el estado es emitiendo una acción, un objeto describiendo que ocurrió. 
3. Para especificar como el **árbol de estado** es transformado por las **acciones**, se utilizan **reducers** puros.

Tengamos en cuenta que :

- A diferencia de [**Flux**](/blog/2025-05-18-Flux.md), en **Redux** no existe el concepto de **Dispatcher**. Esto es porque se basa en funciones puras en vez de emisores de ventos, y las funciones puras son fáciles de componer y no necesitan entidades adicionales para controlarlas

:::tip
**React** proporciona su propio sistema de gestión de estado local : ([**useState**](/docs/programacion/reactjs/hooks/useState.md) y [**useReducer**](/docs/programacion/reactjs/hooks/useReducer.md)), pero cuando la aplicación crece en complejidad y varias partes de la interfaz de usuario necesitan acceder al mismo estado, **Redux** puede ser una solución eficaz.

La instalación de **Redux** se da a través del comando

```javascript
npm install redux
npm install react-redux
```
:::

## Acciones

Las **acciones** son un **bloque de información** que envia datos desde la aplicación al **almacén**, son la única fuente de información y se envian usando **store.dispatch()**.

:::tip
Las **acciones** son **objetos planos de JavaScript**. Una **acción** debe tener una propiedad **type** que indica el **tipo de acción** a realizar. Los **tipos** normalmente son definidos como strings constantes. 

Opcionalmente (pero preferiblemente) se pueden crear **funciones** que retornen un **tipo de acción**.
:::

Para nuestro ejemplo vamos a crear el tipo de acción **ADD_ESTUDIANTE** el cuál tendrá definida una **función** *creadora de la acción* **addEstudiante** que retornará el tipo de acción **ADD_ESTUDIANTE**. 

```javascript title="/src/acciones.js"
export const ADD_ESTUDIANTE = 'ADD_ESTUDIANTE'

export function addEstudiante(estudiante){
    return {
        type : ADD_ESTUDIANTE, 
        payload : estudiante
    }
}
```

## Reducers

Las **acciones** *describen que algo pasó*, pero *no especifican cómo cambió el estado de la aplicación en respuesta*. Esto es trabajo de los **reducers**. El **reducer** es una **función pura** que toma el **estado anterior** y una **acción**, y devuelve en **nuevo estado**.

:::warning
¿Qué nunca deberías hacer dentron de un reducer?

1. Modificar sus argumentos
2. Realizar tareas con efectos secundarios como llamas a un API o transiciones de rutas
3. Llamar una función no pura, por ejemplo Date.now() o Math.random().
:::

En el siguiente ejemplo creamos un objeto **initialState** que contendrá el **modelo** de la aplicación y una función **estudiantesReducer**, el cuál será nuestro **reducer**. La función recibe un parámetro **state** que contendrá el **estado anterior** y un parámetro **action** que contendrá la **acción**. El parámetro **action** contendrá dos campos : **type** almacenará el **tipo de acción** y **payload** contendrá el contenido de la acción. 

En este ejemplo queremos adicionar un nuevo estudiante a la lista de estudiantes definida en **initialState.estudiantes**. Para ellos, se definió el tipo de acción **ADD_ESTUDIANTE**. Cuando invocan al **reducer** y envian **action.type = ADD_ESTUDIANTE**, se hace uso del **operador spread (...)**, el cuál permite expandir elementos de arrays y objetos obteniendo sus elementos individuales. 

```javascript title="/src/reducer.js"
import { ADD_ESTUDIANTE } from "./acciones"

export const initialState = {
    estudiantes: [
    ]
}

function estudiantesReducer(state = initialState, action) {
    switch (action.type) {
        case ADD_ESTUDIANTE:
            return {
                estudiantes: [
                  ...state.estudiantes,
                  action.payload
                ]
              }   
        default:
            return state
    }
}

export default estudiantesReducer
```

## Almacén

Previamente definimos las **acciones** que representan los **hechos** sobre "lo que pasó" y los **reductores** son los que **actualizan** el **estado** de acuerdo a esas **acciones**. El **almacén** es el objeto que los reúne y tiene las siguientes responsabilidades:

1. Contiene el estado de la aplicación;
2. Permite el acceso al estado via **getState()**
3. Permite que el estado sea actualizado via **dispatch(action)**
4. Registra los listeners via **subscribe(listener)**

:::tip
Es importante destacar que sólo tendrás un store en una aplicación **Redux**. Cuando se desea dividir la lógica para el manejo de datos, se debe usar la **composición de reductores** en lugar de muchos stores.
:::

El **almacén** debe ser definido y creado en **main.jsx** y debe ser enviado como parámetro sobre el elemento **Provider** como se muestra a continuación:

```javascript title="/src/main.jsx"
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import { ReduxApp } from './ReduxApp.jsx'
import { Provider } from 'react-redux'
import { legacy_createStore as createStore } from 'redux'
import estudiantesReducer, { initialState } from './reducer'

let store = createStore(estudiantesReducer, initialState)

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <Provider store={store}>
      <ReduxApp />
    </Provider>
  </StrictMode>,
)
```

## Vista

:::tip
Antes de la introducción de **Redux Hooks**, como **useDispatch** en **React Redux** y [**useSelector**](/docs/programacion/reactjs/hooks/useSelector.md), los desarrolladores solían utilizar la función **connect** para conectar **componentes** de **React** al **almacén** de **Redux**. Aunque **connect** cumplía su propósito, a menudo resultaba en un código más complicado de mantener. Con la adopción de **hooks**, como el [**useDispatch**](/docs/programacion/reactjs/hooks/useDispatch.md) en React Redux, se ha vuelto mucho más sencillo lograr la misma funcionalidad de una manera más eficiente y concisa.
:::

Para nuestro ejemplo vamos a crear tres componentes funcionales : **FormEstudiante**,  **ListEstudiantes** y **AppEstudiantes**.  

El componente funcional **FormEstudiante** hace uso del **hook** **useSelector**, **useDispatch** y **useState**. 

- El **hook** **useSelector** le permite elegir un campo del **estado** de la aplicación, en este caso, hace referencia al arreglo de estudiantes definido en **initialState**. 
- El **hook** **useState** le permite crear una **variable de estado** nombrada **nombre** con su función **set** **setNombre**. 
- El **hook** **useDispatch** le permite acceder a las **funciones creadoras de acciones**, en este caso, podrá acceder a la función **addEstudiante** encargada de retornar el tipo de acción **ADD_ESTUDIANTE**. 

El componente funcional **FormEstudiante** definió e implementó dos funciones:

- La función **handleChange** responde al evento **onChange** del campo de texto que contendrá el nombre del estudiante. Su objetivo es actualizar el valor de la **variable de estado** **nombre** haciendo uso de la función **setNombre**. 
- La función **handleClick** responde al evento **onClick** del botón que adiciona un estudiante al arreglo de estudiantes. Su objetivo es llamar al **dispatch** con la **función creadora de acciones** **addEstudiante**. La función **addEstudiante** recibe un parámetro con los datos del estudiante que se almacenarán. Finalmente, la función **handleClick** refresca el valor de la **variable de estado** **nombre**. 

El componente funcional **FormEstudiante** retorna :

- Un parráfo que contiene el total de estudiantes que han sido adicionados. 
- Un campo de texto que contendrá el nombre del estudiante y que invocará la función **handleChange** mediante el evento **onChange**. 
- Un botón que permitirá ejecutar el **dispatch** a través del evento **onClick** el cuál invoca la función **handleClick**. 

```javascript title="/src/FormEstudiante.jsx"
import React from 'react'
import { useSelector, useDispatch } from 'react-redux'
import { useState } from 'react'
import { addEstudiante } from './acciones'

export const FormEstudiante = () => {

    const estudiantes = useSelector(state => state.estudiantes)
    const [nombre, setNombre] = useState('');

    const dispatch = useDispatch();

    const handleChange = (event) => {
        setNombre(event.target.value)
    }

    const handleClick = (event) => {
        dispatch(addEstudiante({
            name: nombre
        }))
        setNombre('');
    }

    return (
        <>
            <p>Hay {estudiantes.length} estudiantes registrados</p>
            <div>
                <label htmlFor="nombre">Nombre : </label>
                <input type="text" id="nombre" name="nombre" value={nombre} onChange={handleChange} />
                <button onClick={handleClick}>Adicionar</button>
            </div>
            
        </>
    )
}
```

El componente funcional **ListEstudiantes** hace uso del **hook** **useSelector** para acceder al **estado** de la aplicación, en especial al arreglo de estudiantes definido en **initialState**. Este componente retorna una lista sin un orden específico donde cada elemento de la lista representará el nombre de cada estudiante. 

```javascript title="/src/ListEstudiantes.jsx"
import React from 'react'
import { useSelector } from 'react-redux'

export const ListEstudiantes = () => {

    const estudiantes = useSelector(state => state.estudiantes)

    return (
        <>
            <p>Los estudiantes registrados son : </p>
            <ul>
                {
                    estudiantes.map(item => {
                        return <li key={item.name} value={item.name}>{item.name}</li>
                    })
                }
            </ul>
        </>
    )
}
```

Es decir que hasta el momento tanto el componente funcional **FormEstudiante** como el componente funcional **ListEstudiantes** hacen referencia al mismo **estado** de la aplicación. En este caso, si se adiciona un estudiante en el componente funcional **FormEstudiante**, no solo se actualizará el componente **FormEstudiante** sino también el componente **ListEstudiantes**. 

Finalmente encapsulamos ambos componentes funcionales : **FormEstudiante** y **ListEstudiante** en **AppEstudiante**

```javascript title="/src/AppEstudiante.jsx"
import React from 'react'
import { FormEstudiante } from './FormEstudiante'
import { ListEstudiantes } from './ListEstudiantes'

export const AppEstudiante = () => {
    return (
        <>
            <FormEstudiante />
            <ListEstudiantes />
        </>
    )
}
```

:::tip**
Se recomienda la lectura de [**Combinación de reductores**](/blog/2025-05-18-Composicion-reducers.md), la cuál nos explica cómo podemos implementar varios reductores y un único almacén para tener organizado nuestro código fuente
:::