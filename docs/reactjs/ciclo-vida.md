---
id: ciclo-vida
title: 13. Ciclo de vida
sidebar_position: 13
author: jeogarod
description: ¿Qué es renderizar un componente? ¿Cada cuánto se renderiza?
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - useState
  - useEffect
  - hooks
last_update:
  date: 04/28/2025
  author: Jeyson Andrés García Rodríguez
---

# 13. Ciclo de vida

El **ciclo de vida** (life cycle) de un componente, representa las **etapas** por las que un componente pasa durante toda su vida, desde la **creación** hasta que es **destruido**. Conocer el ciclo de vida de un componente es muy importante debido a que nos permite saber cómo es que un componente se comporta durante todo su tiempo de vida y nos permite prevenir la gran mayoría de los errores que se provocan en tiempo de ejecución.

## Montaje

En React, el **montaje** es el proceso por medio del cual el componente es **construido** y renderizado en pantalla por primera vez, por lo tanto, se considera montado solo cuando el componente ya es visible en pantalla y ya es parte del **Document Object Model** (**DOM**).

:::tip
Es el lugar perfecto para realizar llamadas a APIs o cargar datos iniciales desde una base de datos.
:::

### Renderizado

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

Una vez que el componente ha sido renderizado inicialmente, puede desencadenar más renderizados **actualizando su estado** con la función **set**. Al actualizar el estado de tu componente, se pone en cola automáticamente un renderizado. Recordemos que la función **set** hace parte de la definición de [useState](./useState). 

Este proceso es recursivo: si el componente actualizado devuelve algún otro componente, React renderizará ese componente a continuación, y si ese componente también devuelve algo, renderizará ese componente a continuación, y así sucesivamente. El proceso continuará hasta que no haya más componentes anidados y React sepa exactamente qué debe mostrarse en pantalla.

:::tip
- Para el renderizado inicial, React utilizará la API del DOM **appendChild()** para poner en pantalla todos los nodos del DOM que ha creado.
- React sólo cambia los nodos del DOM si hay una diferencia entre los renderizados.
- Después de que el renderizado haya terminado y React haya actualizado el DOM, el navegador volverá a pintar la pantalla
:::

## Actualización

En +**React**, la **actualización** es el proceso por medio del cual un componte ya montado es **actualizado**, ya sea por cambiar el **estado** o las **props**.

:::tip
Durante la actualización se comparan las **props** y el **estado** actual con los anteriores para determinar si alguna acción específica debe llevarse a cabo. Por ejemplo, se pueden hacer peticiones a una API para obtener nuevos datos si los **props** cambian o actualizar ciertos valores en función del **estado**.

Si el efecto realiza **tareas asincrónicas** (como llamadas a API), ten en cuenta que no puedes usar **async** directamente en el cuerpo del efecto. En su lugar, puedes definir una **función asincrónica** dentro del efecto y llamarla inmediatamente
:::

## Desmontaje

En **React**, el **desmontaje** es el proceso por medio del cual un componte es **destruido** y finalmente removido del **Document Object Model** (**DOM**), lo que implica que no sea visible en pantalla.

