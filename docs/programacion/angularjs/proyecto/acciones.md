---
id: acciones
title: Acciones
author: jeogarod
description: En este tutorial vamos a entender cómo se puede invocar un método del componente desde el HTML
sidebar_position: 6
tags:
    - angular
    - angularjs
    - npm
last_update:
  date: 12/10/2025
  author: Jeyson Andrés García Rodríguez
---

# Acciones

En la sección anterior creamos un componente nombrado **titulo** y le adicionamos dos variables **nombre** y **apellido**. Los valores de las variables son visualizados desde el **HTML** del componente en unos parráfos. 

Pero, y si fuera un botón?. Un botón requiere de una interacción humana por lo  que al ejecutarlo deberá realizar alguna acción. 

![HTML del componente título](/img/angular-acciones-1.png)

En este caso estamos diciendo que si el usuario da click sobre el botón Saludar, este ejecutará una acción llamada **saludar()**.

![Acción saludar del componente título](/img/angular-acciones-2.png)

Esto implica que se debe implementar el método **saludar()** en la definición del componente **titulo.ts**. 

Podemos también enviar toda la referencia del evento enviando como parámetro al método **saludar($event)**. 

![Parámetro event en el HTML](/img/angular-acciones-3.png)

![Parámetro event en el componente](/img/angular-acciones-4.png)

