---
title: Composición de reductores
description: Cuando se desea dividir la lógica para el manejo de datos en un aplicativo ReactJS que hace uso de Redux, se debe usar la composición de reductores en lugar de muchos stores.
slug: composicion-reductores
authors: 
  - jeogarod
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - redux
  - estado
  - flux
hide_table_of_contents: false
---

# Composición de reductores

Antes de leer este blog es necesario e indispensable que conozcas términos, conceptos y lineamientos como [**Redux**](/docs/programacion/reactjs/frameworks/redux.md) que estan basados en la implementación de la arquitectura [**Flux**](/blog/2025-05-18-Flux.md). 

Recordemos que [**Redux**](/docs/programacion/reactjs/frameworks/redux.md) esta compuesto de cuatro artefactos principales : las **vistas** que ejecutan las **acciones** a través de los **reductores** que pueden crear, consultar, actualizar o eliminar datos definidos en el modelo y gestionados por el **almacén**. 

Según la necesidad del negocio, una aplicación puede tener más de una entidad en el modelo de datos. Por ejemplo, si nuestra aplicación trata de un sistema autogestionable de productos adquiridos por un cliente en una compañía, por lo menos, las entidades cliente y productos deberían existir en el modelo de datos. 

<!-- truncate -->

```javascript
const initialState = {
    cliente:{
        id:0,
        name:"Jeyson",
        age:33,
        email:"jeogarod@gmail.com"
    },
    productos:[
        {
            id:0,
            name:"Salt",
            value:$300
        }
    ]
}
```

Después de definir el modelo de datos, debemos definir el reducer o reductor. Tengamos presente que el reducer es una función JavaScript que recibe el estado actual y una acción y retorna un nuevo estado.

Supongamos que nuestro aplicativo tiene las siguientes capacidades,  funciones o **tipos de acciones**. 

1. Registrar cliente
2. Seleccionar producto
3. De-seleccionar producto
4. Modificar cliente
5. Eliminar cliente
6. Consultar todos los productos seleccionados

Cada **tipo de acción** definiriá su propio **type** y **payload**. Por ejemplo : el tipo de acción **Registrar cliente** define el **type** como **REGISTER_CUSTOMER** y el **payload** como:

```json
{
  id:0,
  name:"Jeyson",
  age:33,
  email:"jeogarod@gmail.com"
}
```

Dado que puede existir más de una entidad de negocio, con uno o varios tipos de acción, se recomienda definir e implementar un reducer por cada entidad de negocio.

En el siguiente ejemplo se definieron e implementaron dos reductores : cliente y producto. 

```javascript
export const clienteReducer = (state = { }, action) => {
    switch (action.type) {
        case "REGISTER_CUSTOMER":
            return { state }

        default:
            return state
    }
}
```

```javascript
export const productosReducer = (state = { productos : []}, action) => {
    switch (action.type) {
        case "ADD_PRODUCTO":
            return [...productos, action.payload]
        default:
            return state
    }
}
```

Cada reductor implementado puede ser combinado creando un único reductor. Esto se logra a través de **combineReducers**. 

```javascript
import { createStore, combineReducers } from 'redux'

const reducer = combineReducers({
    cliente: clienteReducer,
    productos: productosReducer
})
```

Finalmente durante la creación del almacén se envía como argumento a la función el resultado de la combinación de los reductores. 

```javascript
const store = createStore(reducer)
```