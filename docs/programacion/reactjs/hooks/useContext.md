---
id: useContext
title: useContext
sidebar_position: 13
author: jeogarod
description: En este tutorial vamos hacer uso del hook useContext para compartir datos entre un componente padre y uno o varios componentes hijos. 
tags:
  - react
  - reactjs
  - npm
  - vite
  - useContext
  - hooks
last_update:
  date: 05/14/2025
  author: Jeyson Andrés García Rodríguez
---

# useContext

El **hook** **useContext** permite acceder directamente a los valores de un **contexto** sin tener que pasar esos valores por cada nivel de componente de forma explícita. Esta capacidad es extremadamente útil cuando trabajamos con aplicaciones donde es necesario compartir datos, como la autenticación del usuario o las preferencias de un tema, a través de varias capas de la interfaz sin preocuparnos por el **props drilling**. 

El **hook** **useContext** depende de la creación de un **contexto**. Al crear un **contexto**, estamos definiendo un **espacio común** donde se **almacenarán** los **valores** que queremos **compartir entre componentes**.

Supongamos el siguiente ejemplo:

Queremos crear un **contexto** en un aplicativo **ReactJS** que almacene la información de un usuario conectado (**usuario**, **correo**). Para ellos vamos a crear una variable **UserContext** que inicialmente tiene un valor **nulo**.

Este contexto lo vamos a crear en un componente funcional nombrado **Dashboard**. Este componente va recibir como [**props**](/docs/programacion/reactjs/proyecto/props.md) los valores del usuario y correo necesarios para compartir la información del usuario a todos los **componentes hijos** de **Dashboard**. Para este ejemplo, el componente hijo de **Dashboard** será **Usuario**. El componente **Usuario** accede al **contexto** del componente padre en una variable **user** e imprime a través de un parráfo el valor del atributo **usuario** que fue almacenado en el componente **Dashboard**.  

:::tip
1. No olvides exportar la variable **UserContext** para que los componentes hijos pueden obtener una referencia a ella. 
2. Ten presente que no fue modificado el **Provider** del **almacén** de **Redux**. De hecho, el **hook** **useContext** no está definido en un mundo **Redux** sino en un mundo **React**.
3. El **hook** **useContext** funciona perfectamente con **Redux**. 
:::

```javascript title="/src/Usuario.jsx"
import React, { useContext } from 'react'
import { UserContext } from './Dashboard';

export const Usuario = () => {
    const user = useContext(UserContext);
  return (
    <div>
        <p>Hola, {user.usuario}</p>
    </div>
  )
}
```

```javascript title="/src/Dashboard.jsx"
import React, { createContext } from 'react'
import { Usuario } from './Usuario';

export const UserContext = createContext(null);

export const Dashboard = (props) => {
  const user = { usuario: props.usuario, correo: props.email };
  return (
    <UserContext.Provider value={user}>
      <Usuario />
    </UserContext.Provider>
  )
}
```

Supongamos que el componente **Dashboard** será invocado desde **main.jsx**. Recordemos que **Dashboard** recibe dos parámetros en [**props**](/docs/programacion/reactjs/proyecto/props.md). 

```javascript title="/src/main.jsx"
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import { Dashboard } from './Dashboard.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <Dashboard usuario="jeogarod" correo="jeogarod@gmail.com"/>
  </StrictMode>,
)
```