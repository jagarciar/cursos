---
id: useCallback
title: useCallback
sidebar_position: 6
author: jeogarod
description: En este tutorial vamos hacer uso del hook useCallback para memorizar una función en un proyecto ReactJS
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - hooks
  - useCallback
  - memorizacion
last_update:
  date: 04/29/2025
  author: Jeyson Andrés García Rodríguez
---

# useCallback

En el contexto de **React**, **memoización** se refiere a la **optimización** que se puede aplicar para **evitar renderizados innecesarios** y **mejorar el rendimiento de los componentes**. En **React**, cuando los datos o el estado de un componente cambian, este se vuelve a renderizar para reflejar esos cambios en la interfaz de usuario. Sin embargo, en algunos casos, este proceso puede ser ineficiente si se renderizan componentes hijos que no han experimentado cambios en sus propios datos.

La **memorización** en **React** se logra utilizando algunos **hooks** como: [useMemo](/docs/programacion/reactjs/hooks/useMemo.md) o **useCallback**. 

**useCallback** es útil cuando necesitas pasar una **función** como una **propiedad** a un **componente hijo**, y quieres asegurarte que la referencia de la función no cambia innecesariamente. Al **memoizar** la función usando **useCallback**, puedes asegurarte que la referencia de la función sigue siendo siempre el mismo y cuando sus dependencias no cambien.

:::tip
Cuando una referencia de una función cambia, cualquier **componente hijo** que recibe la función como una propiedad se re-renderizará, inclusive si la lógica de la función misma no ha cambiado.

En otras palabras, el simple acto de re-declarar una función (inclusive la misma función exacta), causa que la referencia cambie, y causará que el componente hijo que recibe la función como una propiedad se renderice innecesariamente.
:::

El componente funcional que tomaremos de ejemplo fue nombrado **CallBack**. Este componente definió dos variables de estado nombradas : **contador** y **num** con sus respectivas funciones **set** **setContador** y **setNum**. Adicionalmente, el componente funcional **CallBack** implementó una función **handleChange** la cuál actualiza el valor de la variable de estado : **num** e implementó a través del **hook** **useCallback** la constante **incrementarContador** que recibe un parámetro **num** y ejecuta la función **setContador**. El **hook** **useCallback** solo será ejecutado cuando el valor de la variable de estado **num** sea actualizada. 

El componente funcional **CallBack** retorna en un parráfo el valor de la variable de estado **contador**, una caja de texto la cuál refiere al número que será adicionado al contador. Esta caja de texto lanza la función **handleChange** en el evento **onChange**. Finalmente, el componente funcional **CallBack** retorna un botón encargado de ejecutar la función **memoizada** del **hook** **useCallback**. 

```javascript title="/src/CallBack.jsx"
import React, { useCallback, useState } from 'react'

export const CallBack = () => {

    const [contador, setContador] = useState(0);
    const [num, setNum] = useState(0);

    const handleChange = (event) => {
        setNum(event.target.value)
    }

    const incrementarContador = useCallback((num) => {
        setContador(Number(contador) + Number(num));
    }, [num]);

    return (
        <>
            <div>
                <p>Contador : {contador}</p>
                <input type="number" id="contador" name="contador" onChange={handleChange} value={num} placeholder='Digite el valor a sumar al contador'/>
                <button onClick={() => incrementarContador(num)}>Sumar</button>
            </div>
        </>
    )
}
```

:::danger
Durante la realización de este tutorial tuvimos un inconveniente que arrojaba la siguiente excepción :

**Too many re-renders. React limits the number of renders to prevent an infinite loop.**

Para este caso, nos sucedia porque al definir el botón, asignamos la función **incrementarContador** para la invocación del evento **onClick**. 

```html
<button onClick={incrementarContador(num)}>Sumar</button>
```

La solución es definir una función que invoque a la función **incrementarContador** y que responda al evento **onClick**.

```html
<button onClick={() => incrementarContador(num)}>Sumar</button>
```

Esto sucede dado que la definición base de un **handleClick** es:

```javascript
const handleClick = (event) => { }
```

Mientras que la definición de **incrementarContador** es:

```javascript
const incrementarContador = useCallback((num) => {
        setContador(Number(contador) + Number(num));
    }, [num]);
```
:::