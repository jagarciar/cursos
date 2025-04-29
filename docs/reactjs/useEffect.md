---
id: useEffect
title: 11. useEffect
sidebar_position: 11
author: jeogarod
description: ¿Qué es useEffect? ¿Cómo aporta en un componente funcional?
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - useEffect
  - hooks
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 11. useEffect

El **useEffect** en React es un tipo de hook que se incorporó en la versión de React 16.8. Como su nombre lo indica, este hook nos permite definir efectos. Los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el ciclo de vida de nuestro componente. **useEffect** recibe como parámetro una función que se ejecutará cada vez que nuestro componente se renderice, ya sea por un **cambio de estado**, por **recibir props nuevas** o, y esto es importante, porque es la **primera vez que se monta**.

:::tip
Con el hook **useEffect** en React, también podemos ejecutar trozos en las otras fases del ciclo de vida, ya sea en **updating** o en **unmounting**. En este orden de ideas, el hook **useEffect** en React equivale a una combinación de las funciones **componentDidMount**, **componentDidUpdate** y **componentWillUnmount**.

Para poder usarlo debes importarlo al inicio de nuestro Componente. 

```javascript
import React, { useEffect } from 'react'
```
:::

:::tip
Otro caso de uso muy típico de **useEffect** es la suscripción a los eventos del DOM. Por ejemplo, puede ser útil para subscribirnos al evento de scroll, o el de Intersection Observer para crear fácilmente un componente que sirva de Lazy Load… o simplemente para escuchar el evento resize del window
:::

Supongamos el siguiente ejemplo: Fue creado el componente **Reloj** en el archivo **/src/RelojApp.jsx**. El componente **Reloj** tiene una variable de estado nombrada **segundos**. A su vez, definió la función **setSegundos** para actualizar el valor de la variable **segundos**. 

Se implementó la función **actualizarSegundos** la cuál no recibe ningún parámetro e invoca la función **setSegundos** aumentando el valor de la variable **segundos** en 1. 

Finalmente el componente **Reloj** retorna en un elemento **HTML** un parráfo que concatena el contenido Han transcurrido X segundos, donde X debe ser el valor de la variable **segundos**. 

```javascript title="/src/RelojApp.jsx"
import { useState, useEffect } from 'react';
import React from 'react'

export const Reloj = () => {

  const [segundos, setSegundos] = useState(0)

  const actualizarSegundos = () => {
    setSegundos(segundos + 1);
  }

  return (
    <>
        <p>Han transcurrido {segundos} segundos</p>
    </>
  )
}
```

Si ejecutamos el componente tal cuál como esta hasta el momento, nunca se actualizará la variable de estado **segundos**. Esto dado que no existe ningún evento que desencadene su actualización. 

Partiendo de que es necesario actualizar el valor de la variable **segundos** después de cada renderización del componente **Reloj** podemos adicionar el hook **useEffect**. 

Al referenciar en **useEffect** la función **actualizarSegundos**, cada que se renderice el componente, se invocará la función actualizando el valor de la variable de estado **segundos**. Aún cuando esta alternativa es valida, encontraremos al probar nuevamente que se queda en un loop infinito de renderización. 

```javascript title="/src/RelojApp.jsx"
import { useState, useEffect } from 'react';
import React from 'react'

export const Reloj = () => {

  const [segundos, setSegundos] = useState(0)

  const actualizarSegundos = () => {
    setSegundos(segundos + 1);
  }

  useEffect(actualizarSegundos)

  return (
    <>
        <p>Han transcurrido {segundos} segundos</p>
    </>
  )
}
```

## Loops en la renderización 

Por defecto los efectos se disparan cada vez que se realiza un nuevo renderizado pero podemos evitar que el efecto se vuelva a ejecutar pasándole un segundo parámetro al hook. El parámetro es un array con todos los valores de los que depende nuestro efecto, de forma que sólo se ejecutará cuando ese valor cambie.

Esto se soluciona adicionando al hoook **useEffect** un arreglo de aquellas variables de estado que al cambiar su valor deben ejecutar el evento. 

En nuestro ejemplo, para invocar la función **actualizarSegundos** en el hook **useEffect** dependemos de la actualización del valor de la variable de estado **segundos**. 

```javascript title="/src/RelojApp.jsx"
import { useState, useEffect } from 'react';
import React from 'react'

export const Reloj = () => {

  const [segundos, setSegundos] = useState(0)

  const actualizarSegundos = () => {
    setSegundos(segundos + 1);
  }

  useEffect(actualizarSegundos, [segundos])

  return (
    <>
        <p>Han transcurrido {segundos} segundos</p>
    </>
  )
}
```
Si probamos nuestro componente hasta aquí, pareciera que aún se mantiene la ejecución del loop infinito de renderización pero no es asi. En este caso, después de incluir las variables dependientes, el tiempo de ejecución de la función **actualizarSegundos** es tan rápida que simula o sugiere un loop. 

Adicionemos un timeout a la ejecución para que no se ejecute inmediatamente sino cada 5 segundos:

```javascript title="/src/RelojApp.jsx"
import { useState, useEffect } from 'react';
import React from 'react'

export const Reloj = () => {

  const [segundos, setSegundos] = useState(0)

  const actualizarSegundos = () => {
    setTimeout(() => {  setSegundos(segundos + 5); }, 5000);
  }

  useEffect(actualizarSegundos, [segundos])

  return (
    <>
        <p>Han transcurrido {segundos} segundos</p>
    </>
  )
}
```

## Consumo de API's

En el siguiente ejemplo vamos a consumir una **API REST** expuesta públicamente bajo la URL **https://pokeapi.co/api/v2/type/3**. Esta API esta expuesta bajo un método ***HTTP GET**. El resultado del consumo será almacenado en una variable de estado llamada **pokemones** a través de su función **setPokemones**. 

En este ejemplo, a partir de **useEffect** se invocó el consumo de una **API REST** haciendo uso de **fetch**. La función **fetch** recibe el **endpoint** de la **API** y retorna la respuesta en formato **JSON**. El **hook** **useEffect** dependerá del valor cambiante de la variable de estado **pokemones** para hacer nuevamente el llamado. 

Finalmente se muestran los nombres de los pokemones obtenidos. 

```javascript title="/src/PokemonApp.jsx"
import { useState, useEffect } from 'react';
import React from 'react'

export const Pokemon = () => {

    const url = "https://pokeapi.co/api/v2/type/3";
    const [pokemones, setPokemones] = useState([])

    useEffect(() => {
        fetch(url)
            .then(response => response.json())
            // 4. Setting *dogImage* to the image url that we received from the response above
            .then(data => setPokemones(data.pokemon)).catch((error) => {
                console.error(error);
            })
    }, [pokemones])

    return (
        <>
          Hay {pokemones.length} pokemones
            <ul>
                {pokemones.map((pokemon) =>  <li key={pokemon.pokemon.name} value={pokemon.pokemon.name}>{pokemon.pokemon.name}</li> )}
            </ul>
        </>
    )
}
```
