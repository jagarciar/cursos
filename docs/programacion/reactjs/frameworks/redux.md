---
id: redux
Title: 3. Redux
description: Redux
sidebar_position: 3
author: jeogarod
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - redux
  - estado
  - useState
  - useReducer
last_update:
  date: 02/05/2025
  author: Jeyson Andrés García Rodríguez
---

# 3. Redux

**Redux** es un contenedor de estado para aplicaciones JavaScript especialmente útil en el contexto de aplicaciones de **React**. Fue diseñado para gestionar el **estado** de la aplicación de una manera predecible y centralizada. 

:::tip
**Redux** es un **patrón de arquitectura de datos** que permite manejar el **estado de la aplicación** de una manera predecible. Está pensado para reducir el número de relaciones entre componentes de la aplicación y mantener un flujo de datos sencillo.
:::

**Redux** esta basado en:

1. El **estado** de toda la aplicación se almacena en un objeto de árbol dentro de un solo **store**. Esto facilita la gestión y la comprensión del estado de la aplicación. 
2. La única forma de cambiar el estado es emitiendo una acción (que es un objeto que describe el cambio). Esto garantiza que todas las modificaciones del **estado** sean predecibles y trazables. 
3. Para especificar cómo el estado de la aplicación cambia en respuesta a una acción, se utiliza una función llamada **reducer**. Un **reducer** toma el estado actual y una acción como argumentos y devuelve un nuevo **estado**. 

:::tip
**React** proporciona su propio sistema de gestión de estado local ([**useState**](/docs/programacion/reactjs/hooks/useState.md) [**useReducer**](/docs/programacion/reactjs/hooks/useReducer.md)), pero cuando la aplicación crece en complejidad y varias partes de la interfaz de usuario necesitan acceder al mismo estado, **Redux** puede ser una solución eficaz.
:::