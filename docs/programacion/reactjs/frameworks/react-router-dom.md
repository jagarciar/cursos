---
id: react-router-dom
Title: React Router DOM
description: En este tutorial vamos aprender a usar Redux en un proyecto ReactJS haciendo uso de los hooks useSelector y useDispatch. 
sidebar_position: 4
author: jeogarod
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - react-router-dom
last_update:
  date: 04/15/2025
  author: Jeyson Andrés García Rodríguez
---

# React Router DOM

**React Router** es una librería que se utiliza bastante con **React** y que nos facilita el proceso de definir el **enrutamiento** dentro de nuestra aplicación. 

:::note
**Enrutar** el proceso de mantener **sincronizada** la URL con el contenido de una aplicación, permitiéndonos controlar el flujo de datos de la aplicación.
:::

La ventaja de usar **React Router** sobre otras maneras de crear rutas de navegación es que con ella podremos poner **enlaces** e incluso **redirigir rutas** *sin hacer peticiones nuevas a nuestro servidor*. Normalmente, cada vez que cambia nuestro enlace estamos llamando a nuestro servidor de nuevo, igual que sucede cuando hacemos una recarga. 

:::tip
**React Router** mantiene las peticiones a nivel de navegador. Para ello, utiliza el **HTML API History**, un API de **HTML5** con el que podemos **manipular el historial del navegador**. En términos básicos, lo que hace esta API es permitirnos añadir entradas a nuestro historial para que el usuario pueda navegar hacia atrás y hacia adelante.

Entonces, cuando dirigimos al usuario hacia un nuevo enlace, lo que realmente haremos es añadir una entrada en su historial. Esto quiere decir que proporciona una forma de navegar dentro del navegador, sin hacer llamadas a nuestro servidor o reiniciar nuestra aplicación.

Para instalar **React Router** debemos ejecutar el comando

```javascript
npm install react-router-dom
```
:::

Supongamos el siguiente ejemplo:

Definimos un barra de navegación a través del siguiente componente funcional **NavBar**. **NavBar** retorna junto a **NavLink** el menú de navegación de nuestra aplicación. **NavLink** es un elemento de **React Router** que tiene un atributo **to** sobre el cuál debe ser mencionada la ruta. 

:::tip
Usa **NavLink** para los elementos HTML mientras que **Routes** para la lógica del enrutamiento. **NavLink** debe estar relacionado directamente con las rutas definidas en **Routes**. 
:::

**NavBar** define también las rutas a través de **Routes**. **Routes** debe incluir uno o varios **Route** donde a través del atributo **path** definimos la ruta sobre la cuál se desplegará el componente definido en el atributo **element**. Es decir, si el usuario oprime click sobre el **NavLink** **About** será enrutado al componente **AboutScreen**. 

:::tip
**React Router** le ofrece la opción de que si el usuario quiere acceder a una ruta escrita directamente al navegador y esta no esta definida en **Routes**, se puede implementar una opción **(/*)** para que siempre re-direccione a **/**.
:::

```javascript title="/src/NavBar.jsx"
import React from 'react'
import { Routes, Route, NavLink, Navigate } from "react-router-dom";
import { HomeScreen } from "./HomeScreen";
import { AboutScreen } from "./AboutScreen";

export const Navbar = () => {
    return (
        <>
            <div style={{flexDirection:'column'}}>
                <NavLink to="/" style={{margin:10}}>Home</NavLink>
                <NavLink to="/about" style={{margin:10}}>About</NavLink>
            </div>
            <Routes>
                <Route path="/" element={<HomeScreen />} />
                <Route path="/about" element={<AboutScreen />} />
                <Route path="/*" element={<Navigate to="/" />} />
            </Routes>
        </>
    )
}
```

En el archivo principal **main.jsx** debemos adicionar **BrowserRouter** para que toda nuestra aplicación pueda hacer uso de **NavBar**.  

```javascript title="/src/main.jsx"
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import { BrowserRouter } from 'react-router-dom'
import { Navbar } from './Navbar.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <BrowserRouter>
      <Navbar />
    </BrowserRouter>
  </StrictMode>,
)
```