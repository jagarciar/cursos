---
title: Composición de reductores
description: Cuando se desea dividir la lógica para el manejo de datos en un aplicativo ReactJS que hace uso de Redux, se debe usar la composición de reductores en lugar de muchos stores.
slug: composicion-reductores
sidebar_position: 1
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
last_update:
  date: 05/19/2025
  author: Jeyson Andrés García Rodríguez
hide_table_of_contents: false
---

# Composición de reductores

Recordemos que [**Redux**](/docs/programacion/reactjs/frameworks/redux.md) esta compuesto de cuatro artefactos principales : las **vistas**, las **acciones**, los **reductores** y el **almacén**. Las **vistas**  ejecutan las **acciones** a través de los **reductores**. Los **reductores** crean, consultan, actualizan o eliminan datos definidos en el **modelo** y gestionados por el **almacén**. 

Según la necesidad del negocio, una aplicación puede tener más de una entidad en el modelo de datos. Por ejemplo, si nuestra aplicación trata de un sistema autogestionable de productos adquiridos por un cliente en una compañía, por lo menos, las entidades cliente y productos deberían existir en el modelo de datos. 

<!-- truncate -->

Teniendo en cuenta el ejemplo anterior, podriamos pensar en dos modelos : **initialCustomerState** e **initialProductsState**. 

```javascript
const initialCustomerState = {
    id:0,
    name:"Jeyson",
    age:33,
    email:"jeogarod@gmail.com"
}

const initialProductsState = [
  {
    id:0,
    name:"Salt",
    value:$300
  }
]
```

Cada modelo de datos podría y debería estar asociado a un reductor. Por ejemplo, **clienteReducer** respondería a los tipos de acción asociados al modelo del cliente y **productosReducer** respondería a los tipos de acción asociados al modelo de los productos.  

```javascript
export const clienteReducer = (state = initialCustomerState, action) => {
    switch (action.type) {
        case "REGISTER_CUSTOMER":
            return action.payload;

        default:
            return state
    }
}
```

```javascript
export const productosReducer = (state = initialProductsState, action) => {
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

Finalmente durante la creación del **almacén** se envía como argumento a la función el resultado de la combinación de los reductores. 

```javascript
const store = createStore(reducer)
```

Esto va permitir que tengamos organizado nuestro código con varios reductores y un único almacén. 