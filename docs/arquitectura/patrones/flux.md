---
id: flux
Titule: Flux
description: Flux es un patrón de arquitectura de datos para aplicaciones web que permiten gestionar el estado.
author: jeogarod
sidebar_position: 1
tags:
  - flux
  - patron-software
last_update:
  date: 05/14/2025
  author: Jeyson Andrés García Rodríguez
---

# Flux

**Flux** es una **arquitectura** que facilita la **gestión** y **flujo de datos** de una **aplicación web**. Propone que el camino de los datos tenga un único sentido y que exista una **única fuente de verdad**. De este modo todo el flujo acaba llegando a un sitio que almacena el estado y que se encarga de **actualizar** las **vistas** que están **suscritas** a los cambios que en este tienen lugar.

:::tip
**Flux** propone una arquitectura en la que el flujo de datos es unidireccional. Los **datos** viajan desde la **vista** por medio de **acciones** y llegan a un **Store** desde el cual se actualizará la vista de nuevo.
:::

![Arquitectura Flux](/img/flux.png)

En Resumen, el patrón **flux** sigue el siguiente recorrido:

1. La vista, mediante un evento envía una acción con la intención de realizar un cambio en el estado
2. La acción contiene el tipo y los datos (si los hubiere) y es enviada al dispatcher.
3. El dispatcher propaga la acción al Store y se procesa en orden de llegada.
4. El Store recibe la acción y dependiendo del tipo recibido, actualiza el estado y notifica a las vistas de ese cambio.
5. La vista recibe la notificación y se actualiza con los cambios.

## Vistas

La **vista** serían los **componentes web**, ya sean construidos nativamente, con Polymer, con Angular, React, etc...

## Almacén

Un **almacén** sería lo más parecido al **modelo de la aplicación** dado que guarda los datos/estado de la aplicación.

El **almacén** va a tener cuatro responsabilidades:

1. Almacenar el estado global de la aplicación
2. Dar acceso al estado mediante **store.getState()**
3. Permitir que el estado se actualice mediante **store.dispatch()**
4. Registrar listeners mediante **store.subscribe(listener)**

## Acción

Las **Acciones** son POJOs (**Plain Old JavaScript Objects**) con al menos una propiedad que indica el **tipo de acción** y, de ser necesario, otras propiedades indicando cualquier otro dato necesario para efectuar nuestra acción. Normalmente se usa el formato definido en el **Flux Standard Action (FSA)**.

```javascript
{
    type: 'ADD_TASK',
    payload: {
        id : 1
    },
}
```

Para enviar una acción a nuestro **Store** usamos la función **store.dispatch()** pasando nuestra **acción** como **único parámetro**.

### Creadores de acciones

Estos son simplemente **funciones** que pueden o no recibir parámetros y devuelven una **acción** (un **POJO**), es muy buena idea, para evitar problemas de consistencia, *programar una función por cada tipo de acción* y usarlas en vez de armar nuestros objetos a mano.

```javascript
function addTask(id) {
    return {
        type: 'ADD_TASK',
        payload: {
            id,
        },
    };
}
```

Debido a que normalmente son funciones puras son fáciles de testear. Luego de ejecutar nuestra función, para poder despachar la acción, es simplemente llamar a la función **dispatch(addTask(1))**.

## Dispatcher

Las acciones son enviadas a un dispatcher que se encarga de dispararla o propagarla hasta la Store. La vista es la que se encarga de enviar las acciones al dispatcher.Un dispatcher no es más que un mediador entre la Store o Stores y las acciones. Sirve para desacoplar la Store de la vista, ya que así no es necesario conocer que Store maneja una acción concreta.