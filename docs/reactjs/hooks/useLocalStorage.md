---
id: useLocalStorage
title: 10. useLocalStorage
sidebar_position: 10
author: jeogarod
description: useLocalStorage es un hook de ReactJS que permite estandarizar el almacenamiento local o en caché de las variables de estado o de los elementos HTML
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

# 10. useLocalStorage

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