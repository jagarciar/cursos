---
id: useFetch
title: 9. useFetch
sidebar_position: 9
author: jeogarod
description: useFetch es un hook de ReactJS que permite invocar o consumir API's
tags:
  - react
  - reactjs
  - npm
  - vite
  - useState
  - useEffect
  - useFetch
  - hooks
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 9. useFetch

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
No debes llamar a **Hooks** como [useState](/docs/reactjs/hooks/useState.md) o [useEffect](/docs/reactjs/hooks/useEffect.md) condicionalmente o dentro de ciclos o funciones anidadas. Siempre deben ser utilizados en el nivel superior de tu componente o **Hook personalizado**. Esto asegura que los Hooks se ejecuten en el mismo orden cada vez que tu componente se renderiza, lo cual es crucial para el correcto funcionamiento de React.
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
:::tip
En dado caso el **método HTTP** de la **API REST** no sea **GET** es necesario crear una variable **options** que debe ser enviada a la función **fetch**.
:::

En el siguiente ejemplo, nuestro **hook** **useFetch** recibe tres parámetros : **url**, **method** y **bodyData**. El parámetro **url** representa el endpoint de la **API REST**. El parámetro **method** representa el **método HTTP** (**GET**, **POST**, **PUT**, **DELETE**). El parámetro **bodyData** representa el contenido que debe ser enviado única y opcionalmente en una petición **POST** o **PUT**. 

El **hook** **useFetch** definió en un **useEffect** el llamado a la **API REST**. En el llamado a la función **fetch** se envía la **url** y un objeto nombrado **options**. El objeto **options** tiene tres propiedades : **method**, **headers** y **body**. En la propiedad **method** se almacenará el **método HTTP**. En la propiedad **headers** se incluirá el atributo **Content-type** para definir que la petición y la respuesta serán bajo **JSON**. En la propiedad **body** se almacenará el valor de la variable **bodyData**. 

```javascript title="/src/FetchHook.jsx"
import { useState, useEffect } from 'react';

export const useFetch = (url, method, bodyData = null) => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const options = {
          method: method,
          headers:{
            'Content-type':'application/json; charset=UTF-8'
          },
          body: method == 'GET' || method == 'DELETE' ? null : JSON.stringify(bodyData)
        }
        const response = await fetch(url, options);
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