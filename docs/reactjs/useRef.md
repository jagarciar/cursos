---
id: useRef
title: 12. useRef
sidebar_position: 12
author: jeogarod
description: ¿Qué es useRef?
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - hooks
  - useRef
last_update:
  date: 04/29/2025
  author: Jeyson Andrés García Rodríguez
---

# 12. useRef

El **hook** **useRef** es una función especial en **React** que permite a los desarrolladores acceder y **interactuar** con elementos del **DOM** de manera directa. A diferencia de otros enfoques en **React**, donde la **manipulación** del **DOM** se maneja principalmente a través del **estado** y las **props**, **useRef** proporciona una forma de referenciar elementos de manera más imperativa.

:::tip
A diferencia de otros hooks como [useState](/docs/reactjs/useState.md) o [useEffect](/docs/reactjs/useEffect.md), **useRef** no provoca una actualización del componente cuando cambia. Por lo tanto, **useRef** es ideal para casos en los que necesitamos mantener una referencia constante a un elemento o valor sin causar efectos secundarios en el renderizado del componente.
:::

Supongamos el siguiente ejemplo:

En el archivo **/src/RefApp.jsx** se implementó y exportó el componente funcional **RefApp**. El componente **RefApp** tiene una variable de estado **contador** con su respectiva función **set** **setContador**. Adicionalmente, el componente **RefApp** tiene una función **handleClick** que responde al evento **onClick** de un botón en el retorno del componente. La función **handleClick** se encarga de sumar el valor de la variable de estado **contador** + 1. El componente **RefApp** también definió el **hook** **useEffect** que solo nos va a imprimir por consola cada que se actualiza el valor de la variable **contador**. Finalmente, el componente **RefApp** exporta una caja de texto con el valor de la variable de estado **contador** y un botón que se encarga de ejecutar la función **handleClick**. 

```javascript title="/src/RefApp.jsx"
import React, { useEffect } from 'react'
import { useState } from 'react'

export const RefApp = () => {

    const [contador, setContador] = useState(0)

    const handleClick = (event) => {
        setContador(contador + 1);
    }

    useEffect(() => { console.log("Se actualizó el componente") }, [contador])

    return (
        <>
            <input id="contador" name="contador" type="number"
                value={contador} disabled />
            <button onClick={handleClick}>Sumar +1</button>
        </>
    )
}
```

Es decir, **RefApp** se va a renderizar cada que se actualiza el valor de la variable de estado **contador**. ¿Pero y si no quisieramos renderizar el componente?.

En este caso, debemos importar **useRef** y asignarlo a una variable dentro de nuestro componente funcional, en este caso creamos la variable **inputRef**. La función **handleClick** cumple el mismo objetivo : actualizar el valor de un contador en 1. Sin embargo, a diferencia del anterior ejemplo (cuando usamos **useState** y **useEffect**), al oprimir click sobre el botón que ejecuta la función **handleClick**, no se renderiza el componente, esto dado la actualización del elemento **HTML** es directamente sobre el **DOM**. 


```javascript title="/src/RefApp.jsx"
import React, { useEffect } from 'react'
import { useRef } from 'react'

export const RefApp = () => {

    const inputRef = useRef();

    const handleClick = (event) => {
        if(inputRef.current.value == "")
            inputRef.current.value = 0;
        else
            inputRef.current.value = Number(inputRef.current.value) + 1;
    }

    useEffect(() => { console.log("Se actualizó el componente") }, )

    return (
        <>
            <input id="contador" name="contador" type="number"
                ref={inputRef} disabled/>
            <button onClick={handleClick}>Sumar +1</button>
        </>
    )
}
```