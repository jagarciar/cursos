---
id: custom-hooks
title: 12. Custom hooks
sidebar_position: 12
author: jeogarod
description: ¿Qué son los custom hooks? ¿En qué se diferencian con los hooks?
tags:
  - react
  - reactjs
  - npm
  - vite
  - useState
  - useEffect
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# 12. Custom hooks

Los **custom hooks** en **React** son un tipo de **función JavaScript** que simula el funcionamiento de los **hooks** en **React**. Esta técnica es muy útil siempre que tengamos una lógica que se repite entre varios componentes. En estos casos, podemos sacar esta lógica y aplicarla a un **custom hook**, es decir, una función que ejecute los pasos que necesitamos de manera automática.

:::tip
Los **custom hooks** en **React** son muy útiles para extraer funcionalidades, hacer **refactors** y mantener nuestros componentes más simplificados. Esto es especialmente común cuando tenemos componentes que llaman a una API para obtener un dato, lo meten en un estado y ejecutan una acción determinada con él.
:::