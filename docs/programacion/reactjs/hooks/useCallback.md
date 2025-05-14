---
id: useCallback
title: 6. useCallback
sidebar_position: 6
author: jeogarod
description: El hook useCallback permite memorizar una función en un contexto ReactJS
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - hooks
  - useCallback
  - memorizacion
last_update:
  date: 04/29/2025
  author: Jeyson Andrés García Rodríguez
---

# 6. useCallback

En el contexto de **React**, **memorización** se refiere a la **optimización** que se puede aplicar para **evitar renderizados innecesarios** y **mejorar el rendimiento de los componentes**. En **React**, cuando los datos o el estado de un componente cambian, este se vuelve a renderizar para reflejar esos cambios en la interfaz de usuario. Sin embargo, en algunos casos, este proceso puede ser ineficiente si se renderizan componentes hijos que no han experimentado cambios en sus propios datos.

La **memorización** en **React** se logra utilizando algunos **hooks** como: [useMemo](/docs/programacion/reactjs/hooks/useMemo.md) o **useCallback**. 