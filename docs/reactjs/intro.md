---
sidebar_position: 1
---

# 1. Introducción

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