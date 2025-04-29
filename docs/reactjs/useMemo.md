---
id: useMemo
title: 13. useMemo
sidebar_position: 13
author: jeogarod
description: ¿Qué es useMemo?
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - hooks
  - useMemo
  - memorizacion
last_update:
  date: 04/29/2025
  author: Jeyson Andrés García Rodríguez
---

# 13. useMemo

En el contexto de **React**, **memorización** se refiere a la **optimización** que se puede aplicar para **evitar renderizados innecesarios** y **mejorar el rendimiento de los componentes**. En **React**, cuando los datos o el estado de un componente cambian, este se vuelve a renderizar para reflejar esos cambios en la interfaz de usuario. Sin embargo, en algunos casos, este proceso puede ser ineficiente si se renderizan componentes hijos que no han experimentado cambios en sus propios datos.

La **memorización** en **React** se logra utilizando algunos **hooks** como: **useMemo** o [useCallback](/docs/reactjs/useCallback.md).

**useMemo** es un **hook** que se utiliza para **memorizar** el **resultado** de una **operación costosa de cálculo entre re-renderizaciones de un componente funcional**. Esto ayuda a optimizar el rendimiento al evitar el recálculo innecesario de valores cuando el componente se vuelve a renderizar.