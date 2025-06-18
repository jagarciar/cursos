---
id: react-rick-and-morty
Title: Rick & Morty
description: Paso a paso de la implementación de una aplicación de ejemplo nombrada Rick & Morty que incluirá todos los conceptos que fueron estudiados en la ruta de aprendizaje básica 
sidebar_position: 2
authors: jeogarod
tags:
  - react
  - css
  - reactjs
  - createRoot
  - npm
  - vite
  - bootstrap
  - redux
  - useState
  - useFetch
  - useEffect
  - api-rest
  - api-first
  - hooks
last_update:
  date: 06/04/2025
 author: Jeyson Andrés García Rodríguez
---

# Rick & Morty

En este tutorial vamos a desarrollar desde cero una aplicación nombrada Rick & Morty. El objetivo de esta aplicación es consultar a través de la API los personajes de Rick & Morty, permitirle al usuario seleccionar uno y mostrar algunos datos disponibles del personaje seleccionado.

## Creación del proyecto

Lo primero que debemos hacer es crear un proyecto en **ReactJS**. Para ello y teniendo en cuenta el tutorial [**¿Cómo crear un proyecto ReactJS?**](/docs/programacion/reactjs/proyecto/crear-proyecto.md) debemos ejecutar el siguiente comando:

```javascript
npm create vite@latest
```

Durante la creación vamos a darle un nombre al proyecto, a seleccionar el framework **ReactJS** y la variante **JavaScript + SWC**.  

Después de creado el proyecto, debemos acceder a la carpeta que fue creada e instalar los paquetes y/o dependencias necesarias. Para ello y teniendo en cuenta el tutorial [**¿Cómo crear un proyecto ReactJS?**](/docs/programacion/reactjs/proyecto/crear-proyecto.md) debemos ejecutar el siguiente comando:

```javascript
npm install
```

## Instalación de frameworks adicionales

El proyecto que fue creado previamente tiene los paquetes y/o dependencias necesarias. Sin embargo, para esta aplicación vamos a incluir el uso de [**React Bootstrap**](/docs/programacion/reactjs/frameworks/bootstrap.md) y [**Redux**](/docs/programacion/reactjs/frameworks/redux.md)

Por tal motivo, debemos ejecutar los siguientes comandos:

```javascript
npm install bootstrap
npm install react-bootstrap
npm install redux
npm install react-redux
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
    <title>Rick & Morty</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```
## Requerimientos

- El aplicativo debe obtener los personajes al consumir la API REST **https://rickandmortyapi.com/api/character**. 
- El aplicativo debe mostrar en un combo box los nombres de los personajes. 
- El aplicativo debe obtener la información del personaje seleccionado. El endpoint de la API a consumir será obtenido de la respuesta del consumo de la API REST **https://rickandmortyapi.com/api/character/{id}** donde **{id}** es el identificador del personaje seleccionado. 
- El aplicativo debe mostrar la información del personaje en una tarjeta.
- 
## Diseño

El diseño de la aplicación gozará de la estrategía [**API First**](/blog/api-first) dado que fueron entregados como insumo los endpoint de las API's. Estas API's deben ser consumidas desde los componentes del aplicativo ReactJS. 

El primer endpoint (**https://rickandmortyapi.com/api/character**) es una API expuesta bajo un método **HTTP GET**. Al consumir esta API obtenemos una respuesta en formato **JSON** de la cuál solo los interesa el objeto **results**. El objeto **results** es un arreglo donde cada item contiene dos campos : **id** y **name**. El campo **name** refiere al nombre del personaje y el campo **id** refiere al identificador del personaje. 

```json
{
    {
    "info": {
        "count": 826,
        "pages": 42,
        "next": "https://rickandmortyapi.com/api/character?page=2",
        "prev": null
    },
    "results": [
        {
            "id": 1,
            "name": "Rick Sanchez",
            "status": "Alive",
            "species": "Human",
            "type": "",
            "gender": "Male",
            "origin": {
                "name": "Earth (C-137)",
                "url": "https://rickandmortyapi.com/api/location/1"
            },
            "location": {
                "name": "Citadel of Ricks",
                "url": "https://rickandmortyapi.com/api/location/3"
            },
            "image": "https://rickandmortyapi.com/api/character/avatar/1.jpeg",
            "episode": [
                "https://rickandmortyapi.com/api/episode/1",
                "https://rickandmortyapi.com/api/episode/2",
                "https://rickandmortyapi.com/api/episode/3",
                "https://rickandmortyapi.com/api/episode/4",
                "https://rickandmortyapi.com/api/episode/5",
                "https://rickandmortyapi.com/api/episode/6",
                "https://rickandmortyapi.com/api/episode/7",
                "https://rickandmortyapi.com/api/episode/8",
                "https://rickandmortyapi.com/api/episode/9",
                "https://rickandmortyapi.com/api/episode/10",
                "https://rickandmortyapi.com/api/episode/11",
                "https://rickandmortyapi.com/api/episode/12",
                "https://rickandmortyapi.com/api/episode/13",
                "https://rickandmortyapi.com/api/episode/14",
                "https://rickandmortyapi.com/api/episode/15",
                "https://rickandmortyapi.com/api/episode/16",
                "https://rickandmortyapi.com/api/episode/17",
                "https://rickandmortyapi.com/api/episode/18",
                "https://rickandmortyapi.com/api/episode/19",
                "https://rickandmortyapi.com/api/episode/20",
                "https://rickandmortyapi.com/api/episode/21",
                "https://rickandmortyapi.com/api/episode/22",
                "https://rickandmortyapi.com/api/episode/23",
                "https://rickandmortyapi.com/api/episode/24",
                "https://rickandmortyapi.com/api/episode/25",
                "https://rickandmortyapi.com/api/episode/26",
                "https://rickandmortyapi.com/api/episode/27",
                "https://rickandmortyapi.com/api/episode/28",
                "https://rickandmortyapi.com/api/episode/29",
                "https://rickandmortyapi.com/api/episode/30",
                "https://rickandmortyapi.com/api/episode/31",
                "https://rickandmortyapi.com/api/episode/32",
                "https://rickandmortyapi.com/api/episode/33",
                "https://rickandmortyapi.com/api/episode/34",
                "https://rickandmortyapi.com/api/episode/35",
                "https://rickandmortyapi.com/api/episode/36",
                "https://rickandmortyapi.com/api/episode/37",
                "https://rickandmortyapi.com/api/episode/38",
                "https://rickandmortyapi.com/api/episode/39",
                "https://rickandmortyapi.com/api/episode/40",
                "https://rickandmortyapi.com/api/episode/41",
                "https://rickandmortyapi.com/api/episode/42",
                "https://rickandmortyapi.com/api/episode/43",
                "https://rickandmortyapi.com/api/episode/44",
                "https://rickandmortyapi.com/api/episode/45",
                "https://rickandmortyapi.com/api/episode/46",
                "https://rickandmortyapi.com/api/episode/47",
                "https://rickandmortyapi.com/api/episode/48",
                "https://rickandmortyapi.com/api/episode/49",
                "https://rickandmortyapi.com/api/episode/50",
                "https://rickandmortyapi.com/api/episode/51"
            ],
            "url": "https://rickandmortyapi.com/api/character/1",
            "created": "2017-11-04T18:48:46.250Z"
        }
    ]
}
```

El segundo endpoint dependerá del personaje que seleccione el usuario. Por ejemplo, si el usuario selecciona el personaje Rick Sanchez, debe ser consumida bajo un método **HTTP GET** la API **https://rickandmortyapi.com/api/character/1**. Al consumir esta API obtenemos una respuesta en formato **JSON** de la cuál solo los interesan los campos : **status**, **species**, **gender** e **image**. 

```json
{
    "id": 1,
    "name": "Rick Sanchez",
    "status": "Alive",
    "species": "Human",
    "type": "",
    "gender": "Male",
    "origin": {
        "name": "Earth (C-137)",
        "url": "https://rickandmortyapi.com/api/location/1"
    },
    "location": {
        "name": "Citadel of Ricks",
        "url": "https://rickandmortyapi.com/api/location/3"
    },
    "image": "https://rickandmortyapi.com/api/character/avatar/1.jpeg",
    "episode": [
        "https://rickandmortyapi.com/api/episode/1",
        "https://rickandmortyapi.com/api/episode/2",
        "https://rickandmortyapi.com/api/episode/3",
        "https://rickandmortyapi.com/api/episode/4",
        "https://rickandmortyapi.com/api/episode/5",
        "https://rickandmortyapi.com/api/episode/6",
        "https://rickandmortyapi.com/api/episode/7",
        "https://rickandmortyapi.com/api/episode/8",
        "https://rickandmortyapi.com/api/episode/9",
        "https://rickandmortyapi.com/api/episode/10",
        "https://rickandmortyapi.com/api/episode/11",
        "https://rickandmortyapi.com/api/episode/12",
        "https://rickandmortyapi.com/api/episode/13",
        "https://rickandmortyapi.com/api/episode/14",
        "https://rickandmortyapi.com/api/episode/15",
        "https://rickandmortyapi.com/api/episode/16",
        "https://rickandmortyapi.com/api/episode/17",
        "https://rickandmortyapi.com/api/episode/18",
        "https://rickandmortyapi.com/api/episode/19",
        "https://rickandmortyapi.com/api/episode/20",
        "https://rickandmortyapi.com/api/episode/21",
        "https://rickandmortyapi.com/api/episode/22",
        "https://rickandmortyapi.com/api/episode/23",
        "https://rickandmortyapi.com/api/episode/24",
        "https://rickandmortyapi.com/api/episode/25",
        "https://rickandmortyapi.com/api/episode/26",
        "https://rickandmortyapi.com/api/episode/27",
        "https://rickandmortyapi.com/api/episode/28",
        "https://rickandmortyapi.com/api/episode/29",
        "https://rickandmortyapi.com/api/episode/30",
        "https://rickandmortyapi.com/api/episode/31",
        "https://rickandmortyapi.com/api/episode/32",
        "https://rickandmortyapi.com/api/episode/33",
        "https://rickandmortyapi.com/api/episode/34",
        "https://rickandmortyapi.com/api/episode/35",
        "https://rickandmortyapi.com/api/episode/36",
        "https://rickandmortyapi.com/api/episode/37",
        "https://rickandmortyapi.com/api/episode/38",
        "https://rickandmortyapi.com/api/episode/39",
        "https://rickandmortyapi.com/api/episode/40",
        "https://rickandmortyapi.com/api/episode/41",
        "https://rickandmortyapi.com/api/episode/42",
        "https://rickandmortyapi.com/api/episode/43",
        "https://rickandmortyapi.com/api/episode/44",
        "https://rickandmortyapi.com/api/episode/45",
        "https://rickandmortyapi.com/api/episode/46",
        "https://rickandmortyapi.com/api/episode/47",
        "https://rickandmortyapi.com/api/episode/48",
        "https://rickandmortyapi.com/api/episode/49",
        "https://rickandmortyapi.com/api/episode/50",
        "https://rickandmortyapi.com/api/episode/51"
    ],
    "url": "https://rickandmortyapi.com/api/character/1",
    "created": "2017-11-04T18:48:46.250Z"
}
```

Teniendo en cuenta la respuesta de cada endpoint y los campos que son necesarios, podemos hacer un wireframe de nuestro aplicativo.

![Wireframe del aplicativo Rick & Morty](/img/Rick-Wireframe.png)

Con el wireframe podemos definir nuestros componentes: 

- El componente **App** será el encargado de obtener de la API **https://rickandmortyapi.com/api/character** todos los nombres de los personajes. Este arreglo deberá ser almacenado en el **estado global**.
- El componente **SelectCharacter** incluirá un combo box. Cada opción del combo box representará el nombre de un personaje. Este componente deberá obtener el arreglo del **estado global**. Cada item del arreglo contendrá un campo **id**, **name**, **status**, **species** e **image**. Al seleccionar un personaje, se deberá almacenar en el **estado global**. 
- El componente **SelectCharacter** incluirá el componente **Character**, el cuál deberá ser refrescado cada que se selecciona un personaje. Este componente deberá retornar una tarjeta donde se incluya la imagen, el nombre, el estado y la especie a la cuál pertenece el personaje. Los valores de estos campos serán obtenidos del **estado global**. 

## Desarollo

:::tip
Esta aplicación hará uso del **hook** [**useFetch**](/docs/programacion/reactjs/hooks/useFetch.md). Este **hook** recibe la URL de la API que debe ser consumida y retorna tres campos : **data**, **loading** y **error**.
:::

