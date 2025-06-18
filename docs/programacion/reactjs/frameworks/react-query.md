---
id: react-query
Title: React Query
description: En este tutorial vamos aprender a usar React Query en un proyecto ReactJS
sidebar_position: 6
author: jeogarod
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
  - redux
  - estado
  - flux
  - useQuery
  - react-query
last_update:
  date: 06/18/2025
  author: Jeyson Andrés García Rodríguez
---

# React Query

**React Query**, a menudo llamado **TanStack Query** debido a su fusión con el ecosistema **TANStack** (TAN: Tailwind CSS, Alpine.js y Nuxt.js), es una biblioteca de **administración de estado** y **recuperación de datos** que simplifica enormemente el proceso de manejar **información asíncrona** en aplicaciones React. A diferencia de otros enfoques más tradicionales, **React Query** abraza la asincronía y promueve la obtención de datos en tiempo real de manera eficiente.

:::tip
**React Query** se instala a través de la ejecución del siguiente comando :

```javascript
npm install @tanstack/react-query
```
:::

Cuando utilizas **React Query**, las respuestas de las consultas (queries) a APIs o servicios externos se almacenan automáticamente en una **caché local**. La próxima vez que realices la misma consulta, **React Query** buscará primero en la **caché** para obtener los datos en lugar de hacer una nueva solicitud al servidor. Esto reduce el tráfico de red y mejora el rendimiento de la aplicación al mostrar datos de forma instantánea.

La **caché** de **React Query** está diseñada de manera inteligente y se actualiza automáticamente para mantener los datos frescos. Cuando se realiza una consulta, **React Query** marca los datos almacenados en **caché** como **stale** (**caducados**) y luego realiza una nueva solicitud al servidor para obtener los datos actualizados. Esto permite que la interfaz de usuario muestre datos precisos y actualizados sin la necesidad de realizar peticiones adicionales manualmente.

:::tip
**React Query** maneja automáticamente los estados de carga, éxito o error de las peticiones. Cuando realizas una consulta con [**useQuery**](/docs/programacion/reactjs/hooks/useQuery.md), **React Query** establece automáticamente el estado de **isLoading** mientras se está realizando la consulta. Una vez que la consulta se completa con éxito, los datos se almacenan en el estado **data**. En caso de error, el estado **isError** se establece para manejar errores de red u otros problemas.
:::