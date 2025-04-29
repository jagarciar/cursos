---
id: reactjs-css
Title: 7. CSS
description: ¿Cómo poder modificar los estilos de los componnetes funcionales y/o de clases?
sidebar_position: 7
author: jeogarod
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - css
last_update:
  date: 04/28/2025
  author: Jeyson Andrés García Rodríguez
---

# 7. CSS

Durante la creación de un proyecto en **React** por defecto haciendo uso de **Vite** se crean diferentes archivos y carpetas que fueron explicados en el tutorial [Estructura de un proyecto](/docs/reactjs/estructura-proyecto.md). Dentro de los archivos por defecto que son creados se encuentran algunos con extensión **.css**. Este tipo de archivos contienen la definición de **estilos** de nuestros componentes. 

El archivo **/src/index.css** creado por defecto contiene la definición de los estilos para toda la aplicación y/o proyecto. Sin embargo, **React** permite que también existan definiciones de estilos por cada componente y nos lo demuestra con el archivo **/src/App.css**. 

El componente funcional y/o componente de clase que desee heredar los estilos de un archivo con extensión **.css** debe importar el archivo, por ejemplo:

```javascript
import './index.css'
```

El elemento HTML que desee heredar o hacer uso de una clase **CSS** debe hacer uso del atributo **className**, por ejemplo:

Fue creado el componente **PorfolioApp** el cuál importa la definición de los estilos de un archivo **PorfolioApp.css**. 

```javascript title="/src/PorfolioApp.jsx"
import React from 'react'
import './PorfolioApp.css'

export const PorfolioApp = () => {

    return (
        <>
            <div className='center'>
                <h1>Título</h1>
                <h2 className='id'>Subtitulo</h2>
            </div>
        </>
    )
}
```

**PorfolioApp** retorna en un **div** un título y un subtítulo. El **div** hace referencia a una clase **CSS** llamada **center** y el subtítulo hace referencia a una clase **CSS** llamada **id**. **PorfolioApp.css** también define un estilo estándar para todos los títulos **h1**. 

```css title="/src/PorfolioApp.css"
h1{
    font-size: large;
}

#id{
    font-size:medium;
}

center{
    text-align: center;
    margin: 0 auto;
}
```

Por tal motivo, el componente **PorfolioApp** heredaria todos los estilos que se definieron en **PorfolioApp.css**. Sin embargo, esta no es la única manera de heredar estilos en nuestros componentes. Los estilos también pueden ser definidos dentro de la implementación de un componente, veamos un ejemplo:

Fue modificado el componente **PorfolioApp** para que defina el estilo de un subtítulo **h3** a partir de una lógica de negocio. En el componente se definió una variable llamada **active**, la cuál por defecto tiene el valor **true**. Adicionalmente, el componente definió una segunda variable llamada **style**, la cuál contiene una propiedad llamada **color**. El valor de la propiedad **color** dependerá del valor de la variable **active** (siempre que **active** sea **true** el color será **red**. Si por el contrario, el valor de **active** es diferente de **true**, el color será **black**). 

En este caso para que el subtítulo **h3** herede los estilos deberá hacer uso del atributo **style**. 

```javascript title="/src/PorfolioApp.jsx"
import React from 'react'

export const PorfolioApp = () => {

    const active = true

    const style = {
        color : active ? 'red' : 'black'
    }

    return (
        <>
            <div>
                <h3 style={style}>Estilos</h3>
            </div>
        </>
    )
}
```

Ahora, si no queremos crear una variable para definir el estilo de un elemento **HTML** podemos incluirlo directamente sobre la definición del elemento, veamos un ejemplo:

Fue modificado el componente **PorfolioApp** para que se defina el estilo de un subtítulo **h3** directamente en su definición a través del atributo **style**. En este caso, el tamaño del texto del subtítulo **h3** será **12px**. 

```javascript title="/src/PorfolioApp.jsx"
import React from 'react'

export const PorfolioApp = () => {

    return (
        <>
            <div>
                <h3 style={{fontSize:'12px'}}>Estilos</h3>
            </div>
        </>
    )
}
```

:::tip
Se aconseja que las definiciones de estilos sea en un archivo **css** para que la lectura del código fuente no sea compleja
:::