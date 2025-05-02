---
id: useCounter
title: 8. useCounter
sidebar_position: 8
author: jeogarod
description: useForm es un hook de ReactJS que nos apoya durante la gestión del estado de un formulario
tags:
  - react
  - reactjs
  - npm
  - vite
  - useState
  - useEffect
  - useFetch
  - hooks
  - useCounter
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 8. useCounter

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