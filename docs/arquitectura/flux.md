---
id: flux
Titule: Flux
description: 
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

![Arquitectura Flux](/docs/arquitectura/assets/flux.png)

En Resumen, el patrón **flux** sigue el siguiente recorrido:

1. La vista, mediante un evento envía una acción con la intención de realizar un cambio en el estado
2. La acción contiene el tipo y los datos (si los hubiere) y es enviada al dispatcher.
3. El dispatcher propaga la acción al Store y se procesa en orden de llegada.
4. El Store recibe la acción y dependiendo del tipo recibido, actualiza el estado y notifica a las vistas de ese cambio.
5. La vista recibe la notificación y se actualiza con los cambios.

## Vistas

La **vista** serían los **componentes web**, ya sean construidos nativamente, con Polymer, con Angular, React, etc...

## Store

La **Store** sería lo más parecido al **modelo de la aplicación**. Guarda los datos/estado de la aplicación y en Flux puede existir más de una.

No hay métodos en la Store que permitan modificar los datos en ella, eso se hace a través de **dispatchers** y **acciones**.

## Acción

Un **acción** es simplemente un **objeto JavaScript** que indica una **intención** de realizar algo y que lleva datos asociados si es necesario.

## Dispatcher

Las acciones son enviadas a un dispatcher que se encarga de dispararla o propagarla hasta la Store.

La vista es la que se encarga de enviar las acciones al dispatcher.

Un dispatcher no es más que un mediador entre la Store o Stores y las acciones. Sirve para desacoplar la Store de la vista, ya que así no es necesario conocer que Store maneja una acción concreta.