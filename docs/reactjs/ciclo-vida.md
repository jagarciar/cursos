---
id: ciclo-vida
title: 12. Ciclo de vida
sidebar_position: 12
author: jeogarod
description: ¿Qué es renderizar un componente? ¿Cada cuánto se renderiza?
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - useState
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 12. Ciclo de vida

## Renderizado

:::tip
**Renderizado** significa que React está llamando a tu componente, que es una función. El **JSX** que devuelves de esa función es como una **instantánea de la UI en el tiempo**. Tus props, controladores de eventos y variables locales fueron todos calculados usando su estado en el momento del renderizado.
:::

Teniendo en cuenta la definición de **renderizado**, vamos a explicar qué significa el renderizado inicial y qué sucede después de dicho renderizado. 

El **renderizado inicial** es el cargue inicial de un **componente funcional** y/o **componente de clase**. Frameworks y sandboxes a veces ocultan este código, pero se hace con una llamada a **createRoot** con el nodo **DOM** de destino, y luego con otra llamada a su método **render** con tu componente.

Por ejemplo, Cuando creamos un aplicativo y/o proyecto **React** haciendo uso de **Vite**, se crea un archivo **/src/main.jsx** el cuál invoca la función **createRoot** y **render**. 

```javascript title="/src/main.jsx"
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import { Carro } from './ComponenteApp'

createRoot(document.getElementById('root')).render(
  <StrictMode>

  </StrictMode>,
)
```

Una vez que el componente ha sido renderizado inicialmente, puede desencadenar más renderizados **actualizando su estado** con la función **set**. Al actualizar el estado de tu componente, se pone en cola automáticamente un renderizado. Recordemos que la función **set** hace parte de la definición de [10. useState](./useState). 

Este proceso es recursivo: si el componente actualizado devuelve algún otro componente, React renderizará ese componente a continuación, y si ese componente también devuelve algo, renderizará ese componente a continuación, y así sucesivamente. El proceso continuará hasta que no haya más componentes anidados y React sepa exactamente qué debe mostrarse en pantalla.

:::tip
- Para el renderizado inicial, React utilizará la API del DOM **appendChild()** para poner en pantalla todos los nodos del DOM que ha creado.
- React sólo cambia los nodos del DOM si hay una diferencia entre los renderizados.
- Después de que el renderizado haya terminado y React haya actualizado el DOM, el navegador volverá a pintar la pantalla
:::
