---
id: useMemo
title: useMemo
sidebar_position: 5
author: jeogarod
description: En este tutorial vamos hacer uso del hook useMemo para memorizar el valor de una variable en un proyecto ReactJS
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - hooks
  - useMemo
  - memorizacion
last_update:
  date: 04/29/2025
  author: Jeyson Andrés García Rodríguez
---

# useMemo

En el contexto de **React**, **memorización** se refiere a la **optimización** que se puede aplicar para **evitar renderizados innecesarios** y **mejorar el rendimiento de los componentes**. En **React**, cuando los datos o el estado de un componente cambian, este se vuelve a renderizar para reflejar esos cambios en la interfaz de usuario. Sin embargo, en algunos casos, este proceso puede ser ineficiente si se renderizan componentes hijos que no han experimentado cambios en sus propios datos.

La **memorización** en **React** se logra utilizando algunos **hooks** como: **useMemo** o [useCallback](/docs/programacion/reactjs/hooks/useCallback.md).

**useMemo** es un **hook** que se utiliza para **memorizar** el **resultado** de una **operación costosa de cálculo entre re-renderizaciones de un componente funcional**. Esto ayuda a optimizar el rendimiento al evitar el recálculo innecesario de valores cuando el componente se vuelve a renderizar.

El archivo **/src/MemoApp.jsx** exporta el componente funcional **MemoApp**. El componente **MemoApp** definió dos variables de estado : **factorial** y **clicks**. Cada variable de estado tiene su propia función **set** **setFactorial** y **setClicks**. Adicionalmente, el componente **MemoApp** definió dos funciones que capturan los eventos **onChange** (mediante la función **handleChange**) y **onClick** (mediante la función **handleClick**) del retorno del componente junto a un **hook** **useEffect** el cuál solo mostrará por consola cada que se renderiza el componente. 

Para entender el uso del **hook** **useMemo** se implementó la función **getFactorial** la cuál recibe como parámetro el número sobre el cuál se debe realizar el cálculo. La función **getFactorial** retorna el factorial del número enviado como parámetro. Este resultado es memorizado a través del **hook** **useMemo** en una variable llamada **memorizeFactorial**.

El componente **MemoApp** retorna en un parráfo el número sobre el cuál se debe calcular el factorial, en un segundo parráfo el resultado del cálculo, en una caja de texto el valor de la variable de estado **factorial** la cuál ejecuta la función **handleChange** cuando se dispara el evento **onChange** y un botón para que al disparar el evento **onClick** se ejecute la función **handleClick** la cuál actualiza el valor de la variable de estado **clicks**. 

Es super importante que tengamos presente que el componente **MemoApp** tiene dos variables de estado : **factorial** y **clicks**. El **hook** **useMemo** memoriza el valor del resultado de la función **getFactorial** a partir del valor de la variable de estado **factorial**. Es decir, si la variable de estado **factorial** se actualiza, se vuelve a ejecutar la función **getFactorial**, de lo contrario, no se actualiza. Entonces si ejecutamos la función **handleClick** que actualiza el valor de la variable de estado **clicks** y se mantiene el valor de la variable de estado **factorial**, la función **getFactorial** no es nuevamente ejecutada. 

```javascript title="/src/MemoApp.jsx"
import React from 'react'
import { useState, useMemo, useEffect } from 'react';

export const MemoApp = () => {

    const [factorial, setFactorial] = useState(1);
    const [clicks, setClicks] = useState(0);

    const getFactorial = (num) => {
        console.log("Ejecutando getFactorial()");
        let resultado = 1;
        for (let i = 2; i <= num; i++) {
            resultado *= i;
        }
        return resultado;
    }

    const memorizeFactorial = useMemo(() =>  getFactorial(factorial), [factorial])

    const handleChange = (event) => {
        setFactorial(event.target.value);
    }

    const handleClick = (event) => {
        setClicks(clicks+1);
        console.log("Se han ejecutado "+clicks+" clicks");
    }

    useEffect(() => {console.log("Renderizando..")});

    return (
        <>
            <p>Número : {factorial}</p>
            <p>Factorial : {memorizeFactorial}</p>
            <input type="number" id="fact" name="fact" value={factorial} onChange={handleChange}/>
            <button onClick={handleClick}>Calcular</button>
        </>
    )
}
```

Si el componente **MemoApp** no memorizara a través del **hook** **useMemo** el valor del resultado del cálculo del factorial, cada que se realice un click sobre el botón, se volvería a ejecutar aún si se mantiene el mismo valor de la variable de estado **factorial**. 