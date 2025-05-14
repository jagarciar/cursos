---
id: useEffect
title: useEffect
sidebar_position: 3
author: jeogarod
description: En este tutorial vamos hacer uso del hook useEffect para actualizar el estado de un componente en un proyecto ReactJS
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - useEffect
  - hooks
  - ciclo-vida
  - montaje
  - desmontaje
  - renderizado
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# useEffect

El **useEffect** en React es un tipo de hook que se incorporó en la versión de React 16.8. Como su nombre lo indica, este hook nos permite definir **efectos**. Los efectos en esta librería de JavaScript nos permiten ejecutar un trozo de código según el momento en el que se encuentre el **ciclo de vida** de nuestro componente. **useEffect** recibe como parámetro una función que se ejecutará cada vez que nuestro componente se renderice, ya sea por un **cambio de estado**, por **recibir props nuevas** o, y esto es importante, porque es la **primera vez que se monta**.

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

## Ciclo de vida

El **ciclo de vida** (life cycle) de un componente, representa las **etapas** por las que un componente pasa durante toda su vida, desde la **creación** hasta que es **destruido**. Conocer el ciclo de vida de un componente es muy importante debido a que nos permite saber cómo es que un componente se comporta durante todo su tiempo de vida y nos permite prevenir la gran mayoría de los errores que se provocan en tiempo de ejecución.

### Montaje

En React, el **montaje** es el proceso por medio del cual el componente es **construido** y renderizado en pantalla por primera vez, por lo tanto, se considera montado solo cuando el componente ya es visible en pantalla y ya es parte del **Document Object Model** (**DOM**).

:::tip
Es el lugar perfecto para realizar llamadas a APIs o cargar datos iniciales desde una base de datos.
:::

#### Renderizado

:::tip
**Renderizado** significa que React está llamando a tu componente, que es una función. El **JSX** que devuelves de esa función es como una **instantánea de la UI en el tiempo**. Tus props, controladores de eventos y variables locales fueron todos calculados usando su estado en el momento del renderizado.
:::

Teniendo en cuenta la definición de **renderizado**, vamos a explicar qué significa el renderizado inicial y qué sucede después de dicho renderizado. 

El **renderizado inicial** es el cargue inicial de un **componente funcional** y/o **componente de clase**. Frameworks y sandboxes a veces ocultan este código, pero se hace con una llamada a **createRoot** con el nodo **DOM** de destino, y luego con otra llamada a su método **render** con tu componente.

Por ejemplo, Cuando creamos un aplicativo y/o proyecto **React** haciendo uso de **Vite**, se crea un archivo **/src/main.jsx** el cuál invoca la función **createRoot** y **render**. 

```javascript title="/src/main.jsx"
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import { Carro } from './ComponenteApp'

createRoot(document.getElementById('root')).render(
  <StrictMode>

  </StrictMode>,
)
```

Una vez que el componente ha sido renderizado inicialmente, puede desencadenar más renderizados **actualizando su estado** con la función **set**. Al actualizar el estado de tu componente, se pone en cola automáticamente un renderizado. Recordemos que la función **set** hace parte de la definición de [useState](/docs/programacion/reactjs/hooks/useState.md). 

Este proceso es recursivo: si el componente actualizado devuelve algún otro componente, React renderizará ese componente a continuación, y si ese componente también devuelve algo, renderizará ese componente a continuación, y así sucesivamente. El proceso continuará hasta que no haya más componentes anidados y React sepa exactamente qué debe mostrarse en pantalla.

:::tip
- Para el renderizado inicial, React utilizará la API del DOM **appendChild()** para poner en pantalla todos los nodos del DOM que ha creado.
- React sólo cambia los nodos del DOM si hay una diferencia entre los renderizados.
- Después de que el renderizado haya terminado y React haya actualizado el DOM, el navegador volverá a pintar la pantalla
:::

### Actualización

En +**React**, la **actualización** es el proceso por medio del cual un componte ya montado es **actualizado**, ya sea por cambiar el **estado** o las **props**.

:::tip
Durante la actualización se comparan las **props** y el **estado** actual con los anteriores para determinar si alguna acción específica debe llevarse a cabo. Por ejemplo, se pueden hacer peticiones a una API para obtener nuevos datos si los **props** cambian o actualizar ciertos valores en función del **estado**.

Si el efecto realiza **tareas asincrónicas** (como llamadas a API), ten en cuenta que no puedes usar **async** directamente en el cuerpo del efecto. En su lugar, puedes definir una **función asincrónica** dentro del efecto y llamarla inmediatamente
:::

### Desmontaje

En **React**, el **desmontaje** es el proceso por medio del cual un componte es **destruido** y finalmente removido del **Document Object Model** (**DOM**), lo que implica que no sea visible en pantalla.

## Tips

### Loops en la renderización 

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

### Consumo de API's

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
