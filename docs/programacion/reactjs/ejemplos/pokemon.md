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

# Pokemón

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

## Requerimientos

- El aplicativo debe obtener los nombres de los pokemones al consumir la API REST **https://pokeapi.co/api/v2/type/3**. 
- El aplicativo debe mostrar en un combo box los nombres de los pokemones. 
- El aplicativo debe obtener las habilidades de un pokemon seleccionado. El endpoint de la API a consumir será obtenido de la respuesta del consumo de la API REST **https://pokeapi.co/api/v2/type/3**. 
- El aplicativo debe mostrar las habilidades de un pokemon en una lista sin un orden especifico. 

## Diseño

El diseño de la aplicación gozará de la estrategía [**API First**](/blog/api-first) dado que fueron entregados como insumo los endpoint de las API's. Estas API's deben ser consumidas desde los componentes del aplicativo ReactJS. 

El primer endpoint (**https://pokeapi.co/api/v2/type/3**) es una API expuesta bajo un método **HTTP GET**. Al consumir esta API obtenemos una respuesta en formato **JSON** de la cuál solo los interesa el objeto **pokemon**. El objeto **pokemon** es un arreglo donde cada item contiene dos campos : **name** y **url**. El campo **name** refiere al nombre del pokemon y el campo **url** refiere al endpoint que debe ser consumido para obtener más detalle de dicho pokemon. 

```json
{
    "pokemon": [
        {
            "pokemon": {
                "name": "charizard",
                "url": "https://pokeapi.co/api/v2/pokemon/6/"
            },
            "slot": 2
        },
        {
            "pokemon": {
                "name": "butterfree",
                "url": "https://pokeapi.co/api/v2/pokemon/12/"
            },
            "slot": 2
        },
        {
            "pokemon": {
                "name": "pidgey",
                "url": "https://pokeapi.co/api/v2/pokemon/16/"
            },
            "slot": 2
        },
        {
            "pokemon": {
                "name": "pidgeotto",
                "url": "https://pokeapi.co/api/v2/pokemon/17/"
            },
            "slot": 2
        },
        {
            "pokemon": {
                "name": "pidgeot",
                "url": "https://pokeapi.co/api/v2/pokemon/18/"
            },
            "slot": 2
        }
    ]
}
```

El segundo endpoint dependerá del pokemon que seleccione el usuario. Por ejemplo, si el usuario selecciona el pokemon charizard, debe ser consumida bajo un método **HTTP GET** la API **https://pokeapi.co/api/v2/pokemon/6/**. Al consumir esta API obtenemos una respuesta en formato **JSON** de la cuál solo los interesa el objeto **abilities**. El objeto **abilities** es un arreglo donde cada item contiene el objeto **ability**. El objeto **ability** contiene un campo llamado **name**. Por tal motivo, solo nos interesa obtener todos los **abilities.ability.name** del pokemon seleccionado. 

```json
{
    "abilities": [
        {
            "ability": {
                "name": "blaze",
                "url": "https://pokeapi.co/api/v2/ability/66/"
            },
            "is_hidden": false,
            "slot": 1
        },
        {
            "ability": {
                "name": "solar-power",
                "url": "https://pokeapi.co/api/v2/ability/94/"
            },
            "is_hidden": true,
            "slot": 3
        }
    ]
}
```

Teniendo en cuenta la respuesta de cada endpoint y los campos que son necesarios, podemos hacer un wireframe de nuestro aplicativo.

![Wireframe del aplicativo Pokemon](/img/Pokemon-Wireframe.png)

Con el wireframe podemos definir nuestros componentes: 

- El componente **SelectPokemon** incluirá un combo box. Cada opción del combo box representará el nombre de un pokemon. Los nombres de los pokemones se obtendrán al consumir la API **https://pokeapi.co/api/v2/type/3**. 
- El componente **Abilities** incluirá una lista sin un orden específico. Cada item de la lista será un componente **Ability**. Esta lista será obtenida después de consumir la API según el pokemon seleccionado en el componente **SelectPokemon**.  
- El componente **Ability** representará un item de una lista sin un orden especifico y su valor será una habilidad del pokemon seleccionado en el componente **SelectPokemon**. 

## Desarollo

### Hooks

