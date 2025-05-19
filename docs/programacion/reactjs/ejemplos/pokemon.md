---
id: react-pokemon
Title: Pokemón
description: Paso a paso de la implementación de una aplicación de ejemplo nombrada Pokemon que incluirá todos los conceptos que fueron estudiados en la ruta de aprendizaje básica 
sidebar_position: 1
author: jeogarod
tags:
  - react
  - css
  - reactjs
  - createRoot
  - npm
  - vite
  - bootstrap
  - redux
  - hooks
last_update:
  date: 05/19/2025
  author: Jeyson Andrés García Rodríguez
---

# Aplicación : Pokemón

En este tutorial vamos a desarrollar desde cero una aplicación nombrada Pokemón. El objetivo de esta aplicación es consultar a través de la API los pokemones, permitirle al usuario seleccionar uno y mostrar algunos datos disponibles del pokemon seleccionado. 

## Creación del proyecto

Lo primero que debemos hacer es crear un proyecto en **ReactJS**. Para ello y teniendo en cuenta el tutorial [**¿Cómo crear un proyecto ReactJS?**](/docs/programacion/reactjs/proyecto/crear-proyecto.md) debemos ejecutar el siguiente comando:

```javascript
npm create vite@latest
```

Durante la creación vamos a darle un nombre al proyecto, a seleccionar el framework **ReactJS** y la variante **JavaScript + SWC**.  

![Creación del proyecto Pokemon](/img/Pokemon-App-1.png)

Después de creado el proyecto, debemos acceder a la carpeta que fue creada e instalar los paquetes y/o dependencias necesarias. Para ello y teniendo en cuenta el tutorial [**¿Cómo crear un proyecto ReactJS?**](/docs/programacion/reactjs/proyecto/crear-proyecto.md) debemos ejecutar el siguiente comando:

```javascript
npm install
```

## Instalación de frameworks adicionales

El proyecto que fue creado previamente tiene los paquetes y/o dependencias necesarias. Sin embargo, para esta aplicación vamos a incluir el uso de [**Redux**](/docs/programacion/reactjs/frameworks/redux.md) y [**React Bootstrap**](/docs/programacion/reactjs/frameworks/bootstrap.md). 

Por tal motivo, debemos ejecutar los siguientes comandos:

```javascript
npm install redux
npm install react-redux
npm install bootstrap
npm install react-bootstrap 
```

Dado que este proyecto hará uso de [**React Bootstrap**](/docs/programacion/reactjs/frameworks/bootstrap.md), debemos adicionar en el **index.html** la referencia **CDN** a los estilos gráficos y de paso vamos a modificar el título por Pokemón. 

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <link 
      rel="stylesheet" 
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" 
      integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" 
      crossorigin="anonymous"
    >
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Pokemón</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

