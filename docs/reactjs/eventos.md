---
id: eventos
Titule: 9. Eventos
sidebar_position: 9
description: ¿Cómo ReactJS actua antes los diversos eventos de una sitio web?
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

### Detener la prograpación

Los controladores de eventos reciben un objeto del evento como su único parámetro. Por convención, normalmente es llamado e, que quiere decir “evento”. Puedes usar este objeto para leer información del evento.

Ese objeto del evento también te permite detener la propagación. Si quieres evitar que un evento llegue a los componentes padre, necesitas llamar e.stopPropagation() como este componente Button lo hace:

```javascript
import React from 'react'

export const EventApp = () => {
    
    const handleClick = (event) => { }

    return (
        <>
            <<button onClick={e => {
                e.stopPropagation();
                onClick();
                }}>
                Evento generaodo
                </button>
        </>
    )
}
```