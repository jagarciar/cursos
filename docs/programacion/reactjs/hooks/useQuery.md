---
id: useQuery
title: useQuery
sidebar_position: 14
author: jeogarod
description: En este tutorial vamos hacer uso del hook useQuery para gestionar los datos asíncronos obtenidos de una API
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - hooks
  - useRef
last_update:
  date: 06/18/2025
  author: Jeyson Andrés García Rodríguez
---

# useQuery

**useQuery** es un **hook** que nos permite realizar **peticiones de datos asíncronas**, como una llamada a una API, de manera eficiente y con un manejo automático de estados. Además, [**React Query**](/docs/programacion/reactjs/frameworks/react-query.md) se encarga del **cacheo de los datos**, lo que significa que no tendrás que preocuparte por volver a hacer la misma petición si los datos ya están almacenados y siguen siendo válidos.


:::tip
A través del atributo **staleTime** podemos definir el tiempo de vigencia del resultado obtenido al consumir la API. Es decir, los datos no serán consultados nuevamente sino hasta cuando finalice el tiempo definido. 
:::s