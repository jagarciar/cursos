---
id: custom-hooks
title: 12. Custom hooks
sidebar_position: 12
author: jeogarod
description: ¿Qué son los custom hooks? ¿En qué se diferencian con los hooks?
tags:
  - react
  - reactjs
  - npm
  - vite
  - useState
  - useEffect
  - hooks
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 12. Custom hooks

Un **Custom Hook** es una **función JavaScript** que utiliza otros **Hooks** de React para encapsular lógica de manera que pueda ser reutilizada en varios componentes. Estos hooks no son más que una extensión de los hooks estándar de React, como useRef, [useState](./useState) o [useEffect](./useEffect), permitiéndonos crear nuestra propia lógica que puede ser compartida y reutilizada en varios componentes. Es como un contenedor para la lógica de estado y efectos, permitiendo su reuso sin duplicar código.

:::tip
La **gestión de estados** es uno de los casos de uso más comunes para los **custom hooks** en React. Estos permiten crear **manejadores de estado** que son reutilizables entre diferentes componentes. Por ejemplo, un custom hook podría manejar la lógica de un formulario, almacenando y actualizando valores de los campos de manera eficiente. Esto resulta en un código más limpio y modular, facilitando la mantenibilidad y escalabilidad de las aplicaciones.
:::

:::info
Los **custom hooks** pueden encapsular la lógica para realizar peticiones **HTTP**, manejar respuestas y errores, y gestionar estados de carga. Esto simplifica enormemente los componentes que consumen datos de **APIs**, ya que toda la lógica de red y manejo de datos se abstrae en un hook reutilizable. 
:::

Para crear un **custom hook** en **React**, comenzamos definiendo una función que encapsula la lógica o estado que deseamos reutilizar. Es importante recordar que todos los **hooks** personalizados deben comenzar con **use**, por ejemplo, **useFetch**.

:::info
Un ejemplo práctico podría ser un **hook** de estado que gestione un variable de estado. Este hook utilizaría **useState** para almacenar y actualizar el valor del variable. Cada vez que necesitemos usar esta variable en nuestros componentes, podríamos usar nuestro **custom hook** para manejar esta lógica de manera eficiente y reutilizable.
:::

## useCounter

En el siguiente ejemplo creamos un **custom hook** nombrado **useCounter** en el archivo **/src/useCounter.js**. El **hook** **useCounter** recibe un parámetro nombrado **valorInicial** y tiene una variable de estado nombrada **contador** con su respectiva función **set** **setContador**. Adicionalmente el **hook** **useCounter** definió dos funciones : **incrementar** y **decrementar**. La función **incrementar** recibe un parámetro **valorIncremento** y su objetivo es incrementar el valor de la variable de estado **contador**. La función **decrementar** recibe un parámetro **valorDecremento** y su objetivo es reducir el valor de la variable **contador** (teniendo en cuenta que el valor de la variable **contador** no puede ser menor que 0).

El **hook** **useCouter** no retorna un elemento **HTML**, por el contrario retorna la variable de estado **contador** y las funciones **incrementar** y **decrementar**. 

```javascript title="/src/useCounter.js"
import { useState } from "react"

export const useCounter = (valorInicial = 0) =>{

    const [contador, setContador] = useState(valorInicial)

    const incrementar = (valorIncremento) =>{ 
        setContador(contador + Number(valorIncremento))
    }

    const decrementar = (valorDecremento) =>{ 
        if(Number(valorDecremento) > contador)
            setContador(0)
        else
            setContador(contador - Number(valorDecremento))
    }

    return [
        contador, 
        incrementar, 
        decrementar
    ]
}
```

El **hook** **useCounter** será importado desde el componente funcional **CounterApp**. Por tal motivo el componente **CounterApp** debe definir el retorno del **hook** y la invocación del mismo. Adicionalmente, el componente **CounterApp** tiene una variable de estado **valor** con su respectiva función **set** **setValor**. 

El componente **CounterApp** retorna en un elemento **HTML** un caja de texto que al cambiar su valor modifica el valor de la variable de estado **valor**. El valor de la variable de estado **valor** será enviado como parámetro a las funciones **incrementar** y **decrementar** que son exportadas desde el **hook** **useCounter**. 

```javascript title="/src/CounterApp.jsx"
import React, { useState } from 'react'
import { useCounter } from './useCounter';

export const CounterApp = () => {

  const [contador, incrementar, decrementar] = useCounter(0);
  const [valor, setValor] = useState(0)

  const handleChange = (event) => {
    setValor(event.target.value)
  }

  return (
    <>
        <label htmlFor="valor">Valor : </label>
       <input id="valor" type="number" value={valor} onChange={handleChange}/>
       <p>{contador}</p>
       <button onClick={() => incrementar(valor)}>Incrementar</button>
       <button onClick={() => decrementar(valor)}>Decrementar</button>  
    </>
  )
}
```

## useFetch

En el siguiente ejemplo creamos un **custom hook** nombrado **useFetch** en el archivo **/src/FetchHook.jsx**. El **hook** **useFetch** recibe un parámetro nombrado **url** y tiene tres variables de estado : **data**, **loading** y **error**. Por cada variable de estado, el **hook** define tres funciones : **setData**, **setLoading** y **setError**. 

El **hook** **useFetch** no retorna un elemento **HTML**, por el contrario retorna las variables de estado **data**, **loading** y **error**. Adicionalmente, el **hook** **useFetch** definió un **hook** **useEffect** que invoca o consume una **API REST** a través de **fetch**. 

```javascript title="/src/FetchHook.jsx"
import { useState, useEffect } from 'react';

export const useFetch = (url) => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const result = await response.json();
        setData(result);
      } catch (error) {
        setError(error);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return { data, loading, error };
}
```

:::danger
No debes llamar a **Hooks** como [useState](./useState) o [useEffect](./useEffect) condicionalmente o dentro de ciclos o funciones anidadas. Siempre deben ser utilizados en el nivel superior de tu componente o **Hook personalizado**. Esto asegura que los Hooks se ejecuten en el mismo orden cada vez que tu componente se renderiza, lo cual es crucial para el correcto funcionamiento de React.
:::

Finalmente solo necesitamos reutilizar el **hook** **useFetch** en algún componente que lo requiera:

En el archivo **/src/PokemonApp.jsx** se creo el componente **Pokemon** el cuál hace uso del **hook** **useFetch**. El **hook** recibe la **url** o **endpoint** de la API REST que consumirá o invocará y retorna una bandera que determina si aún está siendo consumida la API, una bandera que determina si se generó un error y/o los datos obtenidos en la respuesta. 

```javascript title="/src/PokemonApp.jsx"
import React from 'react'
import {useFetch} from './FetchHook'

export const Pokemon = () => {

    const {data, loading, error} = useFetch('https://pokeapi.co/api/v2/type/3');

    if (loading) return <p>Loading...</p>;
    if (error) return <p>Error: {error.message}</p>;

    return (
        <div>
            <h1>Data:</h1>
            <pre>{JSON.stringify(data, null, 2)}</pre>
        </div>
    );
}
```

## useLocalStorage

Otro de los hooks que uso frecuentemente es uno que facilita la manipulación del **local storage** del navegador. A continuación podremos ver que se creó el **hook** **useLocalStorage** el cuál recibe dos parámetros : **key** e **initialValue**. El **hook** **useLocalStorage** tiene una variable de estado : **storedValue** la cuál puede ser actualizada a través de la función **setStoredValue**. 

En la definición y uso del **hook** **useState** se obtiene del **local storage** del navegador una llave. Si la encuentra, retorna el valor de esa llave, si no, retorna el valor inicial. Tanto la llave como el valor inicial representan los parámetros del **hook**. 

También encontraremos que se implementó la función **setValue** la cuál actualiza el valor de la variable de estado **storedValue**. 

```javascript title="/src/LocalStorageHook.jsx"
import { useState } from 'react';

export const useLocalStorage = (key, initialValue) => {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      console.error(error);
      return initialValue;
    }
  });

  const setValue = value => {
    try {
      const valueToStore = value instanceof Function ? value(storedValue) : value;
      setStoredValue(valueToStore);
      window.localStorage.setItem(key, JSON.stringify(valueToStore));
    } catch (error) {
      console.error(error);
    }
  };

  return [storedValue, setValue];
}
```

Finalmente solo necesitamos reutilizar el **hook** **useLocalStorage** en algún componente que lo requiera:

En el archivo **/src/PokemonApp.jsx** se creo el componente **Pokemon** el cuál hace uso del **hook** **useLocalStorage**. El **hook** recibe como parámetro el nombre de la llave y el valor que tendrá almacenado en el **local storage** del navegador. 

```javascript title="/src/PokemonApp.jsx"
import React from 'react'
import {useLocalStorage} from './LocalStorageHook'

export const Pokemon = () => {

    const {storedValue, setValue} = useLocalStorage('Pokemon elegido','Picachu');

    return (
        <div>
            <h1>Pokemon elegido : {storedValue}</h1>
        </div>
    );
}
```