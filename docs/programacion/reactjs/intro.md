---
sidebar_position: 1
author : jeogarod
Title: React JS
id: intro
description: Curso orientado a la implementación de aplicativos y/o proyectos en React JS haciendo uso de Vite
---

# Introducción

**React** es una de las bibliotecas **JavaScript** de **código abierto** más populares entre los desarrolladores **Front End**, programadores y testers de software creada por el equipo de la compañía Facebook (Meta). Te permite crear **interfaces de usuario interactivas**, ahorrando tiempo y reduciendo los costos de desarrollo. 

Las aplicaciones de React están hechas a partir de **componentes**. Un **componente** es una pieza de UI (siglas en inglés de interfaz de usuario) que tiene su propia lógica y apariencia. Los componentes representan una fusión de la estructura HTML con la funcionalidad de JavaScript y están escritos con la sintaxis **JSX** (JavaScript XML). A través de **JSX**, se crea una copia de **DOM** (Modelo de Objetos del Documento) llamada **DOM virtual**. Si un componente cambia su estado, React compara el **DOM virtual** con el **DOM real** y aplica este cambio solamente al elemento que ha sido actualizado, sin necesidad de volver a renderizar toda la página.

Los componentes tienen propiedades (**props**), que son sus **atributos** de configuración inmutables. Los estados (**state**) representan un componente en un momento concreto. Existen dos tipos de componentes: **stateful** (con estado) y **stateless** (sin estado). Los componentes con estado dependen de los **datos cambiantes**. A lo largo de su existencia, pasan por una serie de estados, que se le llama **ciclo de vida**. Mientras que los componentes sin estado son más simples, pues únicamente representan la información que les llega como parámetros.

Además, React tiene un **flujo de datos unidireccional**. Es decir, los datos se transmiten en una dirección desde los **componentes superiores** hasta los inferiores. Los **componentes inferiores** procesan los datos, cambian su estado y envían los eventos hacia los componentes superiores que los actualizan.

:::tip
**React** ofrece un “Modo estricto” en el que llama a la función de cada componente dos veces durante el desarrollo. Al llamar a las funciones del componente dos veces, el modo estricto ayuda a encontrar componentes que rompan estas reglas.

```javascript
createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```
:::

## Ruta de aprendizaje

### Básico

Se propone la siguiente ruta de aprendizaje para el curso de ReactJS:

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