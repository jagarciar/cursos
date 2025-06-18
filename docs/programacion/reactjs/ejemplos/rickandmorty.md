---
id: react-rick
Title: Rick
description: Paso a paso de la implementación de una aplicación de ejemplo nombrada Rick and Morty que incluirá todos los conceptos que fueron estudiados en la ruta de aprendizaje básica 
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
  date: 05/19/2025
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

## Desarollo

:::tip
Esta aplicación hará uso del **hook** [**useFetch**](/docs/programacion/reactjs/hooks/useFetch.md). Este **hook** recibe la URL de la API que debe ser consumida y retorna tres campos : **data**, **loading** y **error**.
:::

### Acciones

Dado que nuestra aplicación hará uso de [**Redux**](/docs/programacion/reactjs/frameworks/redux.md), debemos definir las acciones que tendrá. 

Nuestra primera acción será **OBTENER_PERSONAJES** la cuál hace referencia al consumo de la API que retorna todos los personajes de Rick and Morty. La segunda acción es **SELECCIONAR_PERSONAJE** la cuál hace referencia al consumo de la API que retorna la información de un personaje seleccionado. 

```javascript title="actions.js"
export const OBTENER_PERSONAJES = 'OBTENER_PERSONAJES';
export const SELECCIONAR_PERSONAJE = 'SELECCIONAR_PERSONAJE';

export function obtenerPersonajes(personajes) {
    return {
        type: OBTENER_PERSONAJES,
        payload: personajes,
    }
}

export function seleccionarPersonaje(personaje) {
    return {
        type: SELECCIONAR_PERSONAJE,
        payload: personaje,
    }
}
```

Por cada acción se diseñó e implementó una función. Estas funciones retornan el objeto de la acción. 

### Reducers

Dado que nuestra aplicación hará uso de [**Redux**](/docs/programacion/reactjs/frameworks/redux.md), debemos definir los reductores que tendrá.

Esta aplicación tendrá dos reductores : **charactersReducer** y **characterReducer**. 

El reductor **charactersReducer** se encargará de actualizar el estado global de todos los personajes.  

```javascript title="/reducers/charactersReducer.js"
import {OBTENER_PERSONAJES} from '../actions';

const initialState = { /* initial state */ };

const charactersReducer = (state = initialState, action) => {
    switch (action.type) {
        case OBTENER_PERSONAJES:
            return { ...state, ...action.payload };
        default:
            return state;
    }
}

export default charactersReducer;
```

El reductor **characterReducer** se encargará de actualizar el estado global del personaje seleccionado. 

```javascript title="/reducers/characterReducer.js"
import {SELECCIONAR_PERSONAJE} from '../actions';

const initialState = { /* initial state */ };

const characterReducer = (state = initialState, action) => {
    switch (action.type) {
        case SELECCIONAR_PERSONAJE:
            return { ...state, ...action.payload };
        default:
            return state;
    }
}

export default characterReducer;
```

Al tener dos reductores debemos combinarlos en uno solo. 

El reductor **rootReducer** es el encargado de combinar los reductores **characterReducer** y **charactersReducer**. 

```javascript title="/reducers/rootReducer.js"
import  characterReducer from "./characterReducer";
import  charactersReducer  from "./charactersReducer";
import { combineReducers } from "redux";

const rootReducer = combineReducers({
    character: characterReducer,
    characters: charactersReducer
});

export default rootReducer;
```

### Almacén

Dado que nuestra aplicación hará uso de [**Redux**](/docs/programacion/reactjs/frameworks/redux.md), debemos definir el almacén.

El almacén será implementado en el archivo **main.jsx** para que encapsule todo el aplicativo. 

```javascript title="main.jsx"
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'
import { Provider } from 'react-redux'
import rootReducer from './reducers/rootReducer'
import { legacy_createStore as createStore } from 'redux'

let store = createStore(rootReducer)

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </StrictMode>,
)
```

### Vistas

La primera vista de nuestra aplicación será **App.jsx**. En este componente funcional vamos a consumir la API que retorna todos los personajes de Rick & Morty. 

Para consumir la API hará uso de [**useFetch**](/docs/programacion/reactjs/hooks/useFetch.md) y actualizará el estado global haciendo uso de [**useDispatch**](/docs/programacion/reactjs/hooks/useDispatch.md).

```javascript title="App.jsx"
import './App.css'
import { useFetch } from './useFetch';
import { PersonajesList } from './PersonajesList';
import { useDispatch } from 'react-redux';
import { obtenerPersonajes } from './actions';

function App() {

  const { data, loading, error } = useFetch('https://rickandmortyapi.com/api/character')
  const dispatch = useDispatch();

  if (loading) return <h1>Loading...</h1>
  if (error) return <h1>Error: {error.message}</h1>
  if (!data) return <h1>No data found</h1>
  
  dispatch(obtenerPersonajes(data.results));

  return (
   <PersonajesList personajes={data.results}/>
  )
}

export default App
```

Con los personajes obtenidos se actualizará y llamará al componente funcional **PersonajesList.jsx**.

El componente funcional **PersonajesList.jsx** hará uso del hook [**useState**](/docs/programacion/reactjs/hooks/useState.md) y del hook [**useDispatch**](/docs/programacion/reactjs/hooks/useDispatch.md). 

El hook [**useDispatch**](/docs/programacion/reactjs/hooks/useDispatch.md) será disparado cuando seleccionen una de las tarjetas de los personajes (a través del evento **onClick** del botón Seleccionar). La función **handleClick** es la encargada de capturar el evento **onClick** y de buscar en la lista de personajes el personaje seleccionado. La lista de personajes llega como parámetro al componente desde **App.jsx**.  

```javascript title="PersonajesList.jsx**
import Container from 'react-bootstrap/Container';
import Row from 'react-bootstrap/Row';
import Col from 'react-bootstrap/Col';
import Button from 'react-bootstrap/Button';
import Card from 'react-bootstrap/Card';
import { useDispatch} from "react-redux";
import { Personaje } from "./Personaje";
import { useState } from "react";

export const PersonajesList = ({personajes}) => {

    const [show, setShow] = useState(false)
    const dispatch = useDispatch();

    const handleClick = (e) => {
        const personajeSeleccionadoTemp = personajes.find(personaje => personaje.name === e.target.parentElement.firstChild.innerText);
        dispatch({ type: 'SELECCIONAR_PERSONAJE', payload: personajeSeleccionadoTemp });
        setShow(true);
    }

    return (
        personajes.length > 0 ? (
            <>
                <Personaje visible={show}/>
                <Container fluid>
                    <Row>
                        {personajes.map((personaje) => (
                            <Col key={personaje.id}>
                                <Card key={personaje.id} style={{ width: '18rem' }}>
                                    <Card.Img variant="top" src={personaje.image} />
                                    <Card.Body>
                                        <Card.Title>{personaje.name}</Card.Title>
                                        <Card.Text>
                                            {personaje.status == "Alive" ? "Vivo" : "Muerto"} - {personaje.species == "Human" ? "Humano" : "Alien"}
                                        </Card.Text>
                                        <Button variant="primary" onClick={handleClick}>Seleccionar</Button>
                                    </Card.Body>
                                </Card>
                            </Col>
                        )
                        )}
                    </Row>
                </Container>
            </>
        ) :
            <h1>No hay personajes disponibles</h1>

    )
}
```

La variable **show** junto a su función **setShow** permitirá la visualización del componente **Personaje.jsx**. 

El componente **Personaje.jsx** hará uso de los hooks [**useEffect**](/docs/programacion/reactjs/hooks/useEffect.md), [**useDispatch**](/docs/programacion/reactjs/hooks/useDispatch.md) y [**useSelector**](/docs/programacion/reactjs/hooks/useSelector.md). 

El hook [**useSelector**](/docs/programacion/reactjs/hooks/useSelector.md) nos permitirá obtener el personaje seleccionado del estado global. En una primera instancia, no existe ningún personaje seleccionado por lo que tampoco será visible el modal. 

Para actualizar el componente funcional hacemos uso del hook [**useEffect**](/docs/programacion/reactjs/hooks/useEffect.md). Teniendo en cuenta que en una primera instancia no tenemos ningún personaje seleccionado y qué adicionalmente no es posible llamar en el hook [**useEffect**](/docs/programacion/reactjs/hooks/useEffect.md) el hook [**useFetch**](/docs/programacion/reactjs/hooks/useFetch.md), en la implementación de la función hacemos el llamado a la API a través de **fetch**. Cuando se obtiene la información del personaje seleccionado de la API se dispará la actualización del estado global a tráves del hook [**useDispatch**](/docs/programacion/reactjs/hooks/useDispatch.md).

La función **handleClose** nos permite actualizar el valor del parámetro **visible** que habilita o no la visualización del modal. 

:::tip
Hay varios eventos que se activan cuando un modal se cierra. Cada evento se activa después de un cambio de fase específico que el modal experimenta. Este cambio de fase suele ser una etapa de transición en todo su ciclo de vida. Estas etapas pueden ser accesibles pasando propiedades específicas al modal e invocando una función de devolución de llamada.

Cuando el modal empieza a salir de la página, primero se activa la función de retorno **onExiting()**, seguida de la función de retorno **onExited()** cuando el modal termina de salir. Finalmente, se activa la función de retorno **onExit()**, indicando que el modal ha salido completamente de la página.

Otra función que se activa cuando haces clic en el ícono de cerrar del **modal** o haces clic en cualquier lugar del fondo fuera del modal es **onHide()**. 
:::

Dado que existen unas funciones previas a la ejecución del evento **onHide()**, se ve la necesidad de forzar la actualización del componente a través de la función **reload()**. 

```javascript title="Personaje.jsx"
import { useEffect } from 'react'
import { useSelector, useDispatch } from 'react-redux'
import Modal from 'react-bootstrap/Modal';
import Button from 'react-bootstrap/Button';

export const Personaje = ({ visible }) => {

  const personaje = useSelector(state => state.character);
  const dispatch = useDispatch();

  useEffect(() => {
    if (personaje && personaje.id) {
      const url = 'https://rickandmortyapi.com/api/character/' + personaje.id;
      fetch(url).then(response => {
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        return response.json();
      }).then(data => {
        console.log('Personaje cargado:', data);
        dispatch({ type: 'SELECCIONAR_PERSONAJE', payload: data });
      }).catch(error => {
        console.error('Error al cargar el personaje:', error);
      })
    }
  }, [visible]);

 
  const handleClose = () => {
    visible = false;
    reload();
  }

  const reload=()=>window.location.reload();

  return (
    <Modal show={visible} onHide={handleClose}>
      <Modal.Header closeButton>
        <Modal.Title>{personaje.name}</Modal.Title>
      </Modal.Header>
      <Modal.Body>
        <img src={personaje.image} alt={personaje.name} style={{ width: '50%' }} />
        <p><strong>Estado:</strong> {personaje.status == 'Alive' ? 'Vivo' : 'Muerto'}</p>
        <p><strong>Especie:</strong> {personaje.species == "Human" ? "Humano" : "Alien"}</p>
      </Modal.Body>
      <Modal.Footer>
        <Button variant="secondary" onClick={handleClose}>
          Cerrar
        </Button>
      </Modal.Footer>
    </Modal>
  )
}
```

:::tip
Notaran que la implementación se complica un poco dado que nuestras funciones **dispatch** no permiten el llamado asíncrono a las API's. 

Adicionalmente, el componente padre **App.jsx** debe solicitarle a **PersonajesLists.jsx** su actualización, y asi mismo, el componente **PersonajesList.jsx** debe solicitar la actualización de **Personaje.jsx**. Esto obliga el uso de parámetros que refresquen cada componente hijo. 
:::

## Resultado final

![Rick and Morty 1](/img/Rick-Morty-1.png)

![Rick and Morty 1](/img/Rick-Morty-2.png)
 
