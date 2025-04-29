---
id: eventos
Titule: 9. Eventos
sidebar_position: 9
description: ¿Cómo ReactJS actua antes los diversos eventos de una sitio web?
author: jeogarod
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - useState
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 9. Eventos

React te permite añadir **controladores de eventos** a tu **JSX**. Los **controladores de eventos** son tus propias funciones que se ejecutarán en respuesta a interacciones como hacer **clic**, **hover**, **enfocar inputs** en **formularios**, entre otras.

:::tip
Los controladores de eventos también atraparán eventos de cualquier componente hijo que tu componente pueda tener. Decimos que un evento “se expande” o “se propaga” hacia arriba en el árbol de componentes cuando: empieza donde el evento sucedió, y luego sube en el árbol
:::

## 9.1. handleClick

En el siguiente ejemplo creamos un componente funcional llamado **Event**. Este componente contiene un botón el cuál captura un evento de tipo **onClick**. El evento invoca la función **handleClick** que esta implementada previo al retorno. 

En el siguiente ejemplo tenemos un botón que llama a la función **handleClick**. Esta función **handleClick** recibe el parámetro **event** y debe ser desclarado antes del return el componente funcional. 

```javascript
import React from 'react'

export const EventApp = () => {
    
    const handleClick = (event) => { }

    return (
        <>
            <button onClick={handleClick}>Enviar</button>
        </>
    )
}
```

## 9.1. handleChange

En el siguiente ejemplo creamos un componente funcional llamado **Event**. Este componente contiene una caja de texto. El valor de la caja de texto puede variar. El evento invoca la función **handleChange** que esta implementada previo a cada que se adiciiona eliminan o elementos sobre el valor de la caja de texto. 

***tip
¿Quieres entender un poco más este ejemplo? :) Primero debe ir a leer el tutorial [10. useState](/docs/reactjs/useState.md).
:::

En el siguiente ejemplo tenemos un botón que llama a la función **handleChange**. Esta función **handleChange** recibe el parámetro **event** y debe ser desclarado antes del return el componente funcional. 

```javascript
import React, { useState } from 'react'
 
export const EventApp = () => {

    const[palabra, setNuevaPalabara] = useState()
    
    const handleChange = (event) => { 
        setNuevaPalabara(event.target.value)
    }

    return (
        <>
            <input type="text" value={palabra} onChange={handleChange}/>
        </>
    )
}
```

## 9.2 stopPropagation

Los controladores de eventos reciben un objeto del evento como su único parámetro. Por convención, normalmente es llamado e, que quiere decir “evento”. Puedes usar este objeto para leer información del evento.

Ese objeto del evento también te permite detener la propagación. Si quieres evitar que un evento llegue a los componentes padre, necesitas llamar **e.stopPropagation()** como este componente Button lo hace:

```javascript
import React from 'react'

export const EventApp = () => {
    
    const handleClick = (event) => { }

    return (
        <>
            <<button onClick={e => {e.stopPropagation();}}>
                Evento generaodo
                </button>
        </>
    )
}
```

:::tip
A diferencia de las funciones de renderizado, los controladores de eventos no necesitan ser puros, asi que es un buen lugar para cambiar algo; por ejemplo, cambiar el valor de un input en respuesta a la escritura, o cambiar una lista en respuesta a un botón presionado.
:::