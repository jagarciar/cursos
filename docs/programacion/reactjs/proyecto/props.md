---
author: jeogarod
id: props
sidebar_position: 5
description: En este tutorial vamos a entender por qué son importantes las propiedades o argumentos de un componente funcional. 
title: Props
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - jsx
  - props
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 5. Props

Los componentes de **React** utilizan **props** para comunicarse entre sí. Cada componente padre puede enviar información a sus componentes hijos mediante el uso de props. Las **props** pueden parecerte similares a los atributos **HTML**, pero permiten pasar cualquier valor de **JavaScript** a través de ellas, como objetos, arrays y funciones.

Supongamos que tenemos un componente llamado **Carro**. El componente recibe el parámetro **props**. **props** es un objeto que puede tener más de un atributo, por ejemplo: en el componente **Carro**, el parámetro **props** tiene el atributo **nombre**.  

```javascript title="/src/CarroApp.jsx"
import React from 'react'

export const Carro = (props) => {
  return (
    <>
        <div>{props.nombre}</div>
    </>
  )
}
```

Si queremos limitar cuáles son los atributos que **props** puede recibir, debemos modificar la definición del **componente funcional** de la siguiente manera:

```javascript title="/src/CarroApp.jsx"
import React from 'react'

export const Carro = ({nombre}) => {
  return (
    <>
        <div>{nombre}</div>
    </>
  )
}
```

En dado caso sea más de un atributo, se deben enlistar con coma. 

```javascript title="/src/CarroApp.jsx"
import React from 'react'

export const Carro = ({nombre, tipo}) => {
  return (
    <>
        <div>{nombre}</div>
        <div>{tipo}</div>
    </>
  )
}
```

## PropTypes

Si queremos definir unos **parámetros obligatorios** o queremos **restringir el tipo de dato**  debemos importar dentro del componente a **PropTypes**. Por ejemplo, en el siguiente componente se esperan dos parámetros : **nombre** y **cantidadLlantas**. **nombre** está definido como obligatorio dado que en la definición de **propTypes** del componente, se define que es **requerido**. **cantidadLlantas** está definido como opcional. 

Para poder importar a **prop-types** debemos instalar el paquete mediante el siguiente comando:

```javascript
npm install prop-types
```

Es decir que a través de :

```javascript title="/src/CarroApp.jsx"
Carro.propTypes = {
    nombre: PropTypes.string.isRequired,
    cantidadLlantas: PropTypes.number
}
```

Podemos restingir el atributo **nombre** de tipo **requerido** como **string**. Podemos restringir el atributo **cantidadLlantas** de tipo **opcional** como **number**.

```javascript title="/src/CarroApp.jsx"
import React from 'react'
import PropTypes from 'prop-types'

export const Carro = ({nombre, cantidadLlantas}) => {
  return (
    <div>{nombre}</div>
  )
}

Carro.propTypes = {
    nombre: PropTypes.string.isRequired,
    cantidadLlantas: PropTypes.number
}
```

Los **PropTypes** también son objetos con una **clave** y un **par de valores** donde la 'clave' es el nombre de la propiedad, mientras que el valor representa el tipo o la clase por la que se definen.

## Flujo unidireccional de datos

Para transferir el valor de un atributo de una **prop** definido en **componente funcional padre** a un **componente funcional hijo** debemos:

Supongamos el componente **Carro** que tiene dos propiedades : **nombre** , **cantidadLlantas**. El atributo **nombre** es de tipo **string** y es **requerido**. El atributo **cantidadLlantas** es de tipo **numbre** y es **opcional**

```javascript title="/src/CarroApp.jsx"
import React from 'react'
import PropTypes from 'prop-types'

export const Carro = ({nombre, cantidadLlantas}) => {
  return (
    <div>{nombre}</div>
  )
}

Carro.propTypes = {
    nombre: PropTypes.string.isRequired,
    cantidadLlantas: PropTypes.number
}
```

### Importación y uso de componentes

En el archivo **main.jsx** se referencia al **componente padre**. El **componente padre** recibe dos parámetros : **nombre**, de tipo string y es requerido. **cantidadLlantas**, te tipo number y es opcional. 

Encontrarán que al definir el componente **Carro** solo se definió el atributo **nombre**, esto dado que no es obligatorio el atributo **cantidadLlanatas**. 

```javascript title="/src/main.jsx"
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import { Carro } from './CarroApp'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <Carro nombre="Hyndai" />
  </StrictMode>,
)
```

Si quiesieramos enviar todos los atributos:

```javascript title="/src/main.jsx"
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import { Carro } from './CarroApp'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <Carro nombre="Hyndai" cantidadLlantas={4}/>
  </StrictMode>,
)
```

## Valores por defecto

Supongamos que queremos darle valores por defecto al atributo : **nombre**. El atributo  **catidadLlantas** mantendra su definición. Tanto el atributo **nombre** como el atributo **cantidadLlantas** estan descritos dentro del componente **Carro**. 

```javascript title="/src/CarroApp.jsx"
import React from 'react'

export const Carro = ({nombre = "Hyundai", cantidadLlantas}) => {
  return (
    <div>{nombre}</div>
  )
}
```

Finalmente, en el archivo **main.jsx** ya no será necesario enviar el valor del atributo **nombre**, dado que al no ser enviado asumirá el valor por defecto. 

```javascript title="/src/main.jsx"
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import { Carro } from './CarroApp'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <Carro cantidadLlantas={4}/>
  </StrictMode>,
)
```