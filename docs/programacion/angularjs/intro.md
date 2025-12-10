---
sidebar_position: 1
author : jeogarod
Title: Angular JS
id: intro
description: Curso orientado a la implementación de aplicativos y/o proyectos en Angular JS
---

# Introducción

**Angular** es una de las bibliotecas **JavaScript** de **código abierto** más populares entre los desarrolladores **Front End**, programadores y testers de software creada por el equipo de la compañía Google. Te permite crear **interfaces de usuario interactivas**, ahorrando tiempo y reduciendo los costos de desarrollo. 

Las aplicaciones de Angular siguen el patrón de diseño **Modelo-Vista-Controlador (MVC)**, que separa la lógica de presentación de los datos y la interacción del usuario. 

El núcleo de este framework son los **módulos**, **componentes** y **servicios**. Los **módulos** son contenedores que agrupan **componentes** relacionados y otros recursos. Los **componentes** son bloques de construcción que representan diferentes partes de la interfaz de usuario. Los **servicios** proporcionan funcionalidades compartidas y se utilizan para realizar tareas como el manejo de datos o la comunicación con servidores. 

:::tip
**Angular** utiliza **Typescript**, un lenguaje de programación desarrollado por Microsoft. **Typescript** es una mejora de **Javascript** que agrega características de programación orientada a objetos y un sistema de tipos estáticos. 
:::

:::tip
**Angular** posee una característica poderosa llamada : **enlace de datos bidireccional**, la cuál sincroniza automáticamente los datos entre el modelo y la vista. Esto elimina la necesidad de escribir código adicional para mantener la coherencia entre los datos y la interfaz del usuario
:::

## Ruta de aprendizaje

### Básico

Se propone la siguiente ruta de aprendizaje para el curso de AngularJS:

Nuestro desarrollador debe iniciar su ruta de aprendizaje con los primeros pasos en el framework. Para esto deberá leer el tutorial [**¿Cómo crear un proyecto en ReactJS?**](/docs/programacion/reactjs/proyecto/crear-proyecto.md) y [**¿De qué está compuesto nuestro proyecto ReactJS?**](/docs/programacion/reactjs/proyecto/estructura-proyecto.md). 

La finalización de estos dos tutoriales le permitirá a nuestro desarrollador crear los [**Componentes de clase**](/docs/programacion/reactjs/proyecto/componente-clase.md) y/o [**Componentes funcionales**](/docs/programacion/reactjs/proyecto/componente-funcional.md) dentro de un aplicativo ReactJS. Es importante que el tutorial [**Componentes funcionales**](/docs/programacion/reactjs/proyecto/componente-funcional.md) quede muy claro dado que son los únicos tipos de componentes que serán implementados desde el siguiente tutorial hasta el último. 

:::tip 
Tengamos en cuenta que es necesario pero no obligatorio que lean sobre [**JSX**](/docs/programacion/reactjs/frameworks/jsx.md) y [**CSS**](/docs/programacion/reactjs/frameworks/css.md). Seria recomendable dado que [**JSX**](/docs/programacion/reactjs/frameworks/jsx.md) esta directamente relacionada con la sintáxis y [**CSS**](/docs/programacion/reactjs/frameworks/css.md) con los estilos de nuestros componentes. 

Al no ser un tema que esta involucrado directamente con **ReactJS**, el desarrollador será quién opte por decidir si lee o no dicho tutorial.
:::

Después de creado uno o varios [**Componentes funcionales**](/docs/programacion/reactjs/proyecto/componente-funcional.md) por el desarrollador, deberá aprender sobre los [**Props**](/docs/programacion/reactjs/proyecto/props.md) y seguidito a este, sobre los [**Eventos**](/docs/programacion/reactjs/proyecto/eventos.md). El entendimiento de la relación entre los [**Componentes funcionales**](/docs/programacion/reactjs/proyecto/componente-funcional.md), los [**Props**](/docs/programacion/reactjs/proyecto/props.md) y los [**Eventos**](/docs/programacion/reactjs/proyecto/eventos.md) será clave para lo que viene a continuación : **hooks**.  

Los primeros **hooks** que deben ser estudiados por el desarrollador son [**useState**](/docs/programacion/reactjs/hooks/useState.md) y [**useEffect**](/docs/programacion/reactjs/hooks/useEffect.md). Esto dado que estos dos **hooks** son la base principal del **ciclo de vida** y la **gestión del estado** de un aplicativo **ReactJS**.

Si nuestro desarrollador logró entender el uso y la manera de implementar los **hooks** [**useState**](/docs/programacion/reactjs/hooks/useState.md) y [**useEffect**](/docs/programacion/reactjs/hooks/useEffect.md) puede continuar con los siguientes : [**useMemo**](/docs/programacion/reactjs/hooks/useMemo.md) y [**useCallback**](/docs/programacion/reactjs/hooks/useCallback.md). Esto dado que estos dos **hooks** están relacionados directamente con el concepto de **memorización**. 

Inmediatamente sean entendidos a su totalidad, el desarrollador deberá continuar con los **hooks** [**useRef**](/docs/programacion/reactjs/hooks/useRef.md) y [**useContext**](/docs/programacion/reactjs/hooks/useContext.md). Esto dado que los **hooks** restantes son de tipo **custom hook** o **React-Redux hook**. 

Dando continuidad a este curso de ReactJS, nuestra ruta de aprendizaje le extiende el concepto de **hooks** a nuestro desarrollador, permitiéndole definir e implementar los **custom hooks**. El principal y más sencillo **custom hook** por entender es [**useCounter**](/docs/programacion/reactjs/hooks/useCounter.md), continuando con [**useLocalStorage**](/docs/programacion/reactjs/hooks/useLocalStorage.md), [**useForm**](/docs/programacion/reactjs/hooks/useForm.md) y dejando al final [**useFetch**](/docs/programacion/reactjs/hooks/useFetch.md).

:::tip
Recordemos que los **custom hooks** son **hooks** que definen, diseñan e implementan los desarrolladores en un aplicativo. Es decir, no son **hooks** creados directamente en la librería de **ReactJS**. 
:::

¡Vamos super bien! Nuestro desarrollador ya conoce sobre [**Componentes de clase**](/docs/programacion/reactjs/proyecto/componente-clase.md), [**Componentes funcionales**](/docs/programacion/reactjs/proyecto/componente-funcional.md), [**Props**](/docs/programacion/reactjs/proyecto/props.md), [**Eventos**](/docs/programacion/reactjs/proyecto/eventos.md), diversos **hooks** como [**useState**](/docs/programacion/reactjs/hooks/useState.md), [**useEffect**](/docs/programacion/reactjs/hooks/useEffect.md), [**useMemo**](/docs/programacion/reactjs/hooks/useMemo.md), [**useCallback**](/docs/programacion/reactjs/hooks/useCallback.md), [**useRef**](/docs/programacion/reactjs/hooks/useRef.md), [**useContext**](/docs/programacion/reactjs/hooks/useContext.md), [**useCounter**](/docs/programacion/reactjs/hooks/useCounter.md), [**useLocalStorage**](/docs/programacion/reactjs/hooks/useLocalStorage.md), [**useForm**](/docs/programacion/reactjs/hooks/useForm.md) y [**useFetch**](/docs/programacion/reactjs/hooks/useFetch.md).

Todo lo aprendido hasta aquí permite crear aplicaciones en ReactJS. Sin embargo, existen unos frameworks que fueron incluidos durante este curso : [**Redux**](/docs/programacion/reactjs/frameworks/redux.md), [**React Router DOM**](/docs/programacion/reactjs/frameworks/react-router-dom.md) y [**Bootstrap**](/docs/programacion/reactjs/frameworks/bootstrap.md)

Para entender [**Redux**](/docs/programacion/reactjs/frameworks/redux.md) primero debemos aprender sobre los **React-Router hooks** : [**useSelector**](/docs/programacion/reactjs/hooks/useSelector.md) y [**useDispatch**](/docs/programacion/reactjs/hooks/useDispatch.md). Esto dado que tanto el **hook** [**useSelector**](/docs/programacion/reactjs/hooks/useSelector.md) como el **hook** [**useDispatch**](/docs/programacion/reactjs/hooks/useDispatch.md) reemplazan la API de **connect()** y sustituyen el uso de **mapDispatchToProps** y **mapStateToProps**. 

:::tip
Se recomienda hacer uso de los **hooks** [**useSelector**](/docs/programacion/reactjs/hooks/useSelector.md) y [**useDispatch**](/docs/programacion/reactjs/hooks/useDispatch.md) en vez de las funciones **mapDispatchToProps** y **mapStateToProps** de la API **connect()** dado que los **hooks** corrigen algunas excepciones y errores que no son controladas por las funciones. 
:::

[**React Router DOM**](/docs/programacion/reactjs/frameworks/react-router-dom.md) le va enseñar a nuestro desarrollador a definir el enrutamiento del aplicativo y [**Bootstrap**](/docs/programacion/reactjs/frameworks/bootstrap.md) le va enseñar hacer uso de estilos gráficos predefinidos en una librería. 

¡Felicitaciones desarrolladores! si llegaron hasta aquí es porque finalizaron el curso básico de **ReactJS**. Al igual que yo, debes sentir una gran emoción de aprender este framework que estan utilizado en los últimos años. 

:::tip
El resultado final de esta ruta de aprendizaje es una aplicación nombrada : [**Pokemón**](/docs/programacion/reactjs/ejemplos/pokemon.md). En el tutorial encontrarán el paso a paso de la creación, diseño e implementación de la misma. 
:::