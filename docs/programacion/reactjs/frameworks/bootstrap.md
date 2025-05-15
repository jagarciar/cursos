---
id: react-bootstrap
Title: React Bootstrap
description: En este tutorial vamos aprender adicionar Bootstrap en un proyecto ReactJS para darle un aspecto más agradable a nuestro aplicativo. 
sidebar_position: 5
author: jeogarod
tags:
  - react
  - css
  - reactjs
  - createRoot
  - npm
  - vite
  - bootstrap
last_update:
  date: 05/15/2025
  author: Jeyson Andrés García Rodríguez
---

# React Bootstrap 

**Bootstrap** es un popular marco de **CSS** que los desarrolladores utilizan para construir **aplicaciones web responsivas** y con diseño **mobile-first**. **React Bootstrap** es un framework que integra **Bootstrap** con **React**. El objetivo de **React Bootstrap** es reemplazar la naturaleza estática de **Bootstrap** con algo que pueda integrarse bien con el **ciclo de vida** de los componentes de **React**.

Ten en cuenta que :

- **React Bootstrap** entiende el concepto de componentes y facilita el control y uso de los elementos de **Bootstrap**.
- **React Bootstrap** es compatible con los temas de **Bootstrap**. Esto significa que puedes seguir utilizando las **hojas de estilo CSS** de **Bootstrap** en tu aplicación **React**.


:::tip
La instalación de **React Bootstrap** se da a través de la ejecución del comnado

```javascript
npm install react-bootstrap bootstrap
```
:::

El primer cambio que debemos implementar en nuestro aplicativo **ReactJS** es la incorporación de un **link** en la cabecera de **/index.html**. Este link hace referencia a los últimos estilos de la librería obtenidos mediante **CDN**. 

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <!-- Including the bootstrap css via CDN -->
    <link 
      rel="stylesheet" 
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" 
      integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" 
      crossorigin="anonymous"
    >
    <title>Vite + React</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

A continuación solo queda revisar en la [**URL**](https://react-bootstrap.github.io/docs/components/accordion) de la página de **React Bootstrap** los componentes que podemos incluir en nuestro aplicativo. 

Supongamos el siguiente ejemplo : Vamos a crear un componente funcional nombrado **Usuario** el cuál recibirá como **props** (**tipoIdentificacion**, **numIdentificacion**, **nombre**). El componente funcional **Usuario** deberá retornar un componente de tipo [**Cards**](https://react-bootstrap.github.io/docs/components/cards) de **Bootstrap**. 

```javascript title="/src/Usuario.jsx"
import React from 'react'
import Card from 'react-bootstrap/Card';

export const Usuario = (props) => {
  return (
    <Card style={{ width: '18rem' }}>
      <Card.Body>
        <Card.Title>{props.tipoIdentificacion} {props.numIdentificacion}</Card.Title>
        <Card.Text>
          {props.nombre}
        </Card.Text>
      </Card.Body>
    </Card>
  )
}
```

Vamos a llamar desde la raíz al componente funcional **Usuario** enviando los valores de las propiedades **tipoIdentificacion**, **numIdentificacion** y **nombre**. 

```javascript title="/src/main.jsx"
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import { Usuario } from './Usuario.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <Usuario tipoIdentificacion="CC" numIdentificacion="1" nombre="Pepe"/>
  </StrictMode>
)
```