---
id: useForm
title: useForm
sidebar_position: 7
author: jeogarod
description: En este tutorial vamos hacer uso del hook useForm para estandarizar el uso de campos en formularios en proyectos ReactJS
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

# useForm

En el tutorial [Eventos](/docs/programacion/reactjs/proyecto/eventos.md) se explicó el evento **onChange** que debe ser incrustado por cada elemento **HTML** que requiera actualizar el valor del campo con un valor de la variable de estado. 

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