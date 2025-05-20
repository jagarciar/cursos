---
id: react-pokemon
Title: Pokemón
description: Paso a paso de la implementación de una aplicación de ejemplo nombrada Pokemon que incluirá todos los conceptos que fueron estudiados en la ruta de aprendizaje básica 
sidebar_position: 1
authors: jeogarod
image: https://i.imgur.com/mErPwqL.png
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

El proyecto que fue creado previamente tiene los paquetes y/o dependencias necesarias. Sin embargo, para esta aplicación vamos a incluir el uso de [**React Bootstrap**](/docs/programacion/reactjs/frameworks/bootstrap.md). 

Por tal motivo, debemos ejecutar los siguientes comandos:

```javascript
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

- El componente **Pokemon** será el encargado de obtener de la API **https://pokeapi.co/api/v2/type/3** todos los nombres de los pokemones. Este arreglo deberá ser enviado como [**Prop**](/docs/programacion/reactjs/proyecto/props.md) al componente **SelectPokemon**. 
- El componente **SelectPokemon** incluirá un combo box. Cada opción del combo box representará el nombre de un pokemon. Este componente recibirá el arreglo de los pokemones. Cada item del arreglo contendrá un campo **name** y un campo **url**. 
- El componente **SelectPokemon** incluirá el componente **Abilities** y le enviará como [**Prop**](/docs/programacion/reactjs/proyecto/props.md) la url de la API de consulta del pokemon seleccionado. 
- El componente **Abilities** incluirá una lista sin un orden específico. Este componente recibirá la URL del endpoint que debe ser consumido para el pokemon seleccionado. Cada item del arreglo contendrá un campo **name**. Por cada **name** debemos crear un componente Cada item de la lista será un componente **Ability**. 
- El componente **Ability** representará un item de una lista sin un orden especifico y su valor será una habilidad del pokemon seleccionado en el componente **SelectPokemon**. 

## Desarollo

:::tip
Esta aplicación hará uso del **hook** [**useFetch**](/docs/programacion/reactjs/hooks/useFetch.md). Este **hook** recibe la URL de la API que debe ser consumida y retorna tres campos : **data**, **loading** y **error**.
:::

![Diseño](/img/Pokemon-Diseno.svg)

La base de esta aplicación es el consumo inicial de la API que obtiene todos los pokemones. A partir de ello se llena el combo box y dependerá de que el usuario seleccione una de las opciones para que se desencadene el montaje o actualización del componente encargado de consultar las habilidades. De hecho, desde mi punto de vista, la consulta de la API de las habilidades de un pokemon fue la más díficil de implementar (por la dependencia de la acción del usuario). 

Tengamos presente que cada que el usuario seleccione una opción diferente, se refresca el componente padre dado que las variables de estado son actualizadas también. Esto desencadena que el componente hijo deba refrescarse y es el truco para entender el llamado de la segunda API. 

:::tip
¿Por mejorar? Yo creeria que tal vez podriamos usar el **hook** [**useCallback**](/docs/programacion/reactjs/hooks/useCallback.md) para la consulta de todos los pokemones al igual que para la consulta de todas las habilidades de un pokemon. Sin embargo, dado que ambos componentes no tienen otros elementos que impliquen controlar un renderizado, se puede obviar. 
:::

:::tip
¿Por mejorar? Yo creeria que tal vez podriamos usar [**Redux**](/docs/programacion/reactjs/frameworks/redux.md) para almacenar los pokemones y el pokemon seleccionado evitando tener variables de estado con el **hook** [**useState**](/docs/programacion/reactjs/hooks/useState.md). Sin embargo, la situación se complica un poco para el llamado de la segunda API teniendo en cuenta que no es posible llamar un **hook** dentro de una condicional u otro hook. Se espera siempre que se llamen a un alto nivel. 
:::

### Pokemon

El componente **Pokemon** fue diseñado e implementado en el archivo **/src/Pokemon.jsx**. Este componente hace uso del **hook** [**useFetch**](/docs/programacion/reactjs/hooks/useFetch.md), el cuál recibe la URI de la API que será consumida inicialmente **https://pokeapi.co/api/v2/type/3** y retorna el resultado (en el campo **data**), el estado de finalización del consumo (en el campo **loading**) y el detalle de un **error** (siempre que se capture uno en el **hook**).

El componente **Pokemon** solo renderizará el componente **SelectPokemon** cuando el campo **data** del **hook** [**useFetch**](/docs/programacion/reactjs/hooks/useFetch.md) retorne algún valor. En ese momento, le enviará como [**Props**](/docs/programacion/reactjs/proyecto/props.md) el arreglo de pokemones obtenido previamente. 

```javascript title="/src/Pokemon.jsx"
import React from 'react'
import { SelectPokemon } from './SelectPokemon'
import { useFetch } from './useFetch';

export const Pokemon = () => {

    const { data, loading, error } = useFetch('https://pokeapi.co/api/v2/type/3');
    
    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error.message}</p>;
    return (
        <SelectPokemon pokemones={data.pokemon} />
    )
}
```

### SelectPokemon 

El componente **SelectPokemon** fue diseñado e implementado sobre el archivo **/src/SelectPokemon.jsx**. Este componente recibe mediante [**Props**](/docs/programacion/reactjs/proyecto/props.md) el arreglo de pokemones y por cada item un objeto llamado **pokemon** el cuál contiene el campo **name** y el campo **url**.

El componente **SelectPokemon** tiene dos variables de estado : **urlEndpointPokemon** y **pokemon** con sus respectivas funciones **set** : **setURL** y **setPokemon**. Recordemos que las variables de estado son creadas a partir del **hook** [**useState**](/docs/programacion/reactjs/hooks/useState.md). 

El componente **SelectPokemon** retorna bajo un [**Container**](https://react-bootstrap.github.io/docs/layout/grid) el combo box ([**DropdownButton**](https://react-bootstrap.github.io/docs/components/dropdowns/)) y el componente **Abilities**. 

El combo box ([**DropdownButton**](https://react-bootstrap.github.io/docs/components/dropdowns/)) responde al evento **onSelect** a través de la ejecución de la función **handleSelect**. Es decir, cada que un usuario seleccione un pokemon, el evento **onSelect** disparará la función **handleSelect**, la cuál buscará el pokemon seleccionado en el arreglo de pokemones que llegaron como [**Props**](/docs/programacion/reactjs/proyecto/props.md). Al ser encontrado, se actualizaran los variables de estado : **urlEndpointPokemon** y **pokemon** mediante las funciones **setURL** y **setPokemon**. Esto generará que el componente se renderice nuevamente y a su vez renderice los componentes hijos (como el componente **Abilities**).

En este caso cuando aún no ha finalizado el consumo la API, el componente **SelectPokemon** retornará un parráfo con la palabra **Loading...**. Por el contrario, si se generó una excepción durante la integración, el retorno del componente será un parráfo con el mensaje del error capturado. 

```javascript title="/src/SelectPokemon.jsx"
import React, {  useState } from 'react'
import DropdownButton from 'react-bootstrap/DropdownButton';
import Container from 'react-bootstrap/Container';
import { SelectItemPokemon } from './SelectItemPokemon';
import { Abilities } from './Abilities';

export const SelectPokemon = ({ pokemones }) => {

    const [urlEndpointPokemon, setURL] = useState('');
    const [pokemon, setPokemon] = useState('');

    const handleSelect = (event) => {
        pokemones.map((pokemon) => {
            if (pokemon.pokemon.name == event) {
                setPokemon(pokemon.pokemon.name)
                setURL(pokemon.pokemon.url);
            }
        })
        
    }

    return (
        <Container fluid>
            <DropdownButton id="dropdown-basic-button" title="Seleccione un pokemon" onSelect={handleSelect}>
                {
                    pokemones.map(Pokemon => <SelectItemPokemon key={Pokemon.pokemon.name} name={Pokemon.pokemon.name} />)
                }
            </DropdownButton>
            <Abilities pokemon={pokemon} urlEndpoint={urlEndpointPokemon} />
        </Container>
    )
}
```

### Abilities 

El componente **Abilities** puede ser muy símil al componente **Pokemon** dado que se integran con un sistema externo a través del consumo de una API REST. En este caso **Abilities** recibe dos parámetros como [**Props**](/docs/programacion/reactjs/proyecto/props.md) : **pokemon** y **urlEndpoint**. El parámetro **pokemon** contendrá el nombre del pokemon seleccionado. El parámetro **urlEndpoint** contendrá la URL de la API REST que debe ser consumida según el pokemon seleccionado. 

Dado que el componente **Abilities** debe integrarse con un sistema externo a través del consumo de una API hará uso del **hook** [**useFetch**](/docs/programacion/reactjs/hooks/useFetch.md). Tengamos presente que el **hook** [**useFetch**](/docs/programacion/reactjs/hooks/useFetch.md) retorna la respuesta (en el campo **data**), el estado del consumo de la API (en el campo **loading**) y un campo con el error generado (siempre que se capture una excepción durante el consumo).

El componente **Abilities** retorna bajo un [**Container**](https://react-bootstrap.github.io/docs/layout/grid) un componente nombrado [**ListGroup**](https://react-bootstrap.github.io/docs/components/dropdowns/) y un parráfo con el nombre del pokemón que fue seleccionado. Este componente modela una lista des-organizada.

Cada item del [**ListGroup**](https://react-bootstrap.github.io/docs/components/dropdowns/) será un componente hijo **Ability** el cuál recibe como [**Props**](/docs/programacion/reactjs/proyecto/props.md) el nombre de la habilidad del pokemón. 

En este caso cuando aún no ha finalizado el consumo la API o se generó una excepción durante la integración, el retorno del componente será vacío. 

```javascript title="/src/Abilities.jsx"
import React from 'react'
import ListGroup from 'react-bootstrap/ListGroup';
import Container from 'react-bootstrap/Container';
import { Ability } from './Ability';
import { useFetch } from './useFetch';

export const Abilities = ({ pokemon, urlEndpoint }) => {

    const { data, loading, error } = useFetch(urlEndpoint);
    let abilities = data && data.abilities ? data.abilities : [];

    if (loading) return;
    if (error) return;
    return (
        <Container style={{marginTop:20}}>
            <p>Las habilidades de {pokemon} son :</p>
            <ListGroup>
                {abilities.map(ability => <Ability key={ability.ability.name} name={ability.ability.name} />)}
            </ListGroup>
        </Container>
    )
}
```

### Ability

El componente **Ability** recibe como [**Props**](/docs/programacion/reactjs/proyecto/props.md) el nombre de la habilidad del pokemon que fue seleccionado y lo retorna bajo un componente [**ListGroup.Item**](https://react-bootstrap.github.io/docs/components/list-group). 

```javascript title="/src/Ability.jsx"
import React from 'react'
import ListGroup from 'react-bootstrap/ListGroup';

export const Ability = ({name}) => {

  return (
    <ListGroup.Item key={name}>{name}</ListGroup.Item>
  )
}
```

## Resultado

El resultado final de nuestro aplicativo es el siguiente:

![Resultado](/img/Pokemon-Resultado.png)