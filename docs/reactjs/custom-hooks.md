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
  - useFetch
  - hooks
  - useForm
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 12. Custom hooks

Un **Custom Hook** es una **función JavaScript** que utiliza otros **Hooks** de React para encapsular lógica de manera que pueda ser reutilizada en varios componentes. Estos hooks no son más que una extensión de los hooks estándar de React, como useRef, [useState](/docs/reactjs/useState.md) o [useEffect](/docs/reactjs/useEffect.md), permitiéndonos crear nuestra propia lógica que puede ser compartida y reutilizada en varios componentes. Es como un contenedor para la lógica de estado y efectos, permitiendo su reuso sin duplicar código.

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
No debes llamar a **Hooks** como [useState](/docs/reactjs/useState.md) o [useEffect](/docs/reactjs/useEffect.md) condicionalmente o dentro de ciclos o funciones anidadas. Siempre deben ser utilizados en el nivel superior de tu componente o **Hook personalizado**. Esto asegura que los Hooks se ejecuten en el mismo orden cada vez que tu componente se renderiza, lo cual es crucial para el correcto funcionamiento de React.
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

## useForm

En el tutorial [Eventos](/docs/reactjs/eventos.md) se explicó el evento **onChange** que debe ser incrustado por cada elemento **HTML** que requiera actualizar el valor del campo con un valor de la variable de estado. 

:::tip
Un campo de un formulario cuyos valores son controlados por React es denominado “
**componente controlado**.
:::

En el siguiente archivo **/src/FormApp.jsx** se implementó el componente funcional **FormApp**. Este componente definió dos variables de estado : **nombre** y **edad**. Cada variable de estado tiene su propia función **set** **setNombre** y **setEdad**. Adicionalmente, el componente definió tres funciones : **handleSubmit**, **handleChangeNombre** y **handleChangeEdad**. Las funciones **handleChangeNombre** y **handleChangeEdad** actualizan el valor de la variable de estado : **nombre** o **edad** según corresponda. La función **handleSubmit** previene el refresh que se ejecuta por defecto al enviar un formulario. 

```javascript title="/src/FormApp.jsx"
import React from 'react'
import { useState } from 'react';

export const FormApp = () => {

    const [nombre, setNombre] = useState('');
    const [edad, setEdad] = useState(0);

    const handleChangeNombre = (event) => {
        setNombre(event.target.value);
    };

    const handleChangeEdad = (event) => {
        setEdad(Number(event.target.value));
    };

    const handleSubmit = (event) => {
        event.preventDefault();
        console.log('Se envió el formulario');
    };

    return (
        <>
            <form onSubmit={handleSubmit}>
                <div>
                    <label htmlFor="nombre">Nombre : </label>
                    <input type="text" id="nombre" onChange={handleChangeNombre} value={nombre}/>
                </div>
                <div>
                    <label htmlFor="edad">Edad : </label>
                    <input type="number" id="edad" onChange={handleChangeEdad} value={edad}/>
                </div>
                <button onSubmit={handleSubmit}>Enviar</button>
            </form>
        </>
    )
}
```

Como podemos ver, existe una definición transversal para las funciones orientadas a cumplir con el objetivo del evento **onChange**. Todas las funciones que capturan este evento actualizan el valor de una variable de estado. Por esta razón, esta definición puede ser llevada a un **hook** al cuál nombraremos **useForm**. 

El **hook** **useForm** recibe un parámetro de tipo objeto con los valores iniciales del formulario y define la variable de estado **values** y su función **set** **setValues** para almacenar y actualizar los campos del formulario. Adicionalmente, el **hook** **useForm** definió la función **handleChange** para capturar el nombre del campo del formulario y el valor.  El **hook** **useForm** retorna el arreglo con los valores de los campos del formulario. En otras palabras, se esta generalizando la creación de las variables de estado de cada campo de un formulario y su función **set**. 

```javascript title="/src/useForm.jsx"
import { useState } from "react";

export const useForm = (initialValues) => {
    const [values, setValues] = useState(initialValues);

    const handleChange = (event) => {
      console.log(event.target.name);
      setValues({
        ...values,
        [event.target.name]: event.target.value
      });
    }

    return [
        values,
        handleChange
    ];
}
```
El componente **FormApp** ya no creará las dos variables de estado : **nombre** y **edad**, ni tampoco las funciones **set** **setNombre** y **setEdad**. Por el contrario, el componente **FormApp** importará el **hook** **useForm**, el cuál exporta : **values** y **handleChange**. Cada elemento **HTML** del formulario que retorna el componente **FormApp** deberá incluir el atributo **name** y deberá invocar la función **handleChange** en el evento **onChange**. 

```javascript title="/src/FormApp.jsx"
import React from 'react'
import { useState } from 'react';
import { useForm } from './useForm';

export const FormApp = () => {

    const initialState = { nombre: "", edad: 0 };
    const [values, handleChange] = useForm(initialState);

    const handleSubmit = (event) => {
        event.preventDefault();
        console.log(values);
    };

    return (
        <>
            <form onSubmit={handleSubmit}>
                <div>
                    <label htmlFor="nombre">Nombre : </label>
                    <input type="text" id="nombre" name="nombre" onChange={handleChange}/>
                </div>
                <div>
                    <label htmlFor="edad">Edad : </label>
                    <input type="number" id="edad" name="edad" onChange={handleChange}/>
                </div>
                <button>Enviar</button>
            </form>
        </>
    )
}
```