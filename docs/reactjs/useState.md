---
id: reactjs-useState
Titule: 10. useState
sidebar_position: 10
description: ¿Qué es el estado en un aplicativo ReactJS? ¿Cómo almacenarlo? ¿Como actualizarlo?
author: jeogarod
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - useState
  - hooks
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 10. useState

Los componentes a menudo necesitan cambiar lo que se muestra en pantalla como resultado de una interacción. Escribir dentro de un formulario debería actualizar el campo de texto, hacer clic en “siguiente” en un carrusel de imágenes debería cambiar la imagen que es mostrada; hacer clic en un botón para comprar un producto debería actualizar el carrito de compras. En los ejemplos anteriores los componentes deben “recordar” cosas: el campo de texto, la imagen actual, el carrito de compras. En React, a este tipo de memoria de los componentes se le conoce como **estado**.

Como memoria de un componente, el **estado** no es como una **variable regular** que desaparece después de que tu función devuelva un valor. Cuando React llama a tu componente, te da una **instantánea del estado** para ese renderizado en particular. Tu componente devuelve una instantánea de la interfaz de usuario con un nuevo conjunto de accesorios y controladores de eventos en su JSX, todo calculado usando los valores de estado de ese renderizado.

En React, **useState**, así como cualquier otra función que empiece con "use", se le conoce como **Hook**. Los **Hooks** son funciones especiales que sólo están disponibles mientras React está renderizando. **useState** es un **Hook** de **React** que permite agregar una **variable de estado** a un **componente**.

:::tip
Las **variables de estado** pueden parecerse a las variables normales de JavaScript en las que se puede leer y escribir. Sin embargo, el estado se comporta más como una instantánea. Al asignarlo no se cambia la variable de estado que ya tienes, sino que se **desencadena** una rerenderizado.
:::

En el siguiente ejemplo hemos creado el componente **Carro**. El componente **Carro** tiene dos props : **nombre** y **tipo** y dos variables : **name** y **type**. Las dos variables definen su función **set** (aquella que permite actualizar el valor de la variable). En nuestro caso tenemos dos funciones : **setName** y **setType**. 

Por tal motivo, **useState** le permite al componente **Carro** tener dos estados : **name** y **type**. 

```javascript title="/src/CarroApp.jsx"
import { useState } from 'react';
import React from 'react'

export const Carro = ({nombre, tipo}) => {

  const [name, setName] = useState(nombre)
  const [type, setType] = useState(tipo)
  
  return (
    <div>{name}</div>
  )
}
```

Para poder entender el uso del **setName** y **setType** debemos adicionar interacciones a nuestro componente. El texto que se digite sobre una caja de texto asumirá el valor de la variable **name**. El texto que se seleccione sobre una lista de opciones asumirá el valor de la variable **type**. 

:::note
Las variables locales no persisten entre renderizaciones
:::

Para actualizar estos valores debemos implementar dos funciones que respondan al evento : **onChange**. La primera función : **handleChangeName** actualizará el valor de la variable **name** haciendo uso del **setName**. La segunda función : **handleChangeType** actualizará el valor de la variable **type** haciendo uso del **setType**.

:::tip
El valor de una variable de estado nunca cambia dentro de un renderizado, incluso si el código de tu controlador de evento es asíncrono. Dentro del onClick de ese renderizado, el valor de number sigue siendo 0 incluso después de que se llama a setNumber(number + 5). Su valor se “fijó” cuando React “tomó la instantánea” de la UI al llamar a tu componente.
:::

```javascript title="/src/CarroApp.jsx"
import { useState } from 'react';
import React from 'react'

export const Carro = ({nombre, tipo}) => {

  const [name, setName] = useState(nombre)
  const [type, setType] = useState(tipo)

  const handleChangeName = (event) => {
    setName(event.target.value)
  }

  const handleChangeType = (event) => {
    setType(event.target.value)
  }
  
  return (
    <>
        <input type="text" value={name} onChange={handleChangeName} />
        <select value={type} onChange={handleChangeType}>
            <option value="CC">CC</option>
            <option value="CE">CE</option>
            <option value="TI">TI</option>
        </select>
    </>
  )
}
```



