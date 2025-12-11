---
id: forms
title: Formularios
author: jeogarod
description: En este tutorial vamos a entender cómo se puede mapear los campos de un formulario con el modelo de un componente
sidebar_position: 10
tags:
    - angular
    - angularjs
    - npm
last_update:
  date: 12/10/2025
  author: Jeyson Andrés García Rodríguez
---

# Formularios

Antes de iniciar este tutorial es necesario crear un componente nombrado **Login** y garantizar que fueron creados los archivos **login.ts**, **login.spec.ts**, **login.html** y **login.css**. 

En el siguiente ejemplo vamos a crear un formulario que simule la autenticación de un usuario a través de un usuario y contraseña. 

Lo primero que debemos hacer es crear una interface que mapee los dos campos que permiten una autenticación : usuario y contraseña. Esta interface se va crear dentro del componente **Login** bajo el nombre : **login.model.ts**. 

![Creación de la interface](/img/angular-forms-1.png)

Lo segundo es crear una **señal** **loginModel** y una variable **loginForm** con los valores inicializados.

![Mapeo con el modelo](/img/angular-forms-2.png)

Finalmente desde el **HTML** del componente podemos referenciar a los valores haciendo uso de la directiva **[field]**. En caso de requerir obtener el valor debemos invocar el método **.value()**. 

![Mapeo con el modelo](/img/angular-forms-3.png)