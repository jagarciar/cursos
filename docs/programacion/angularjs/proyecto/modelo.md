---
id: modelo
title: Modelo
author: jeogarod
description: En este tutorial vamos a entender cómo se relaciona el modelo de un componente en el HTML del mismo
sidebar_position: 5
tags:
    - angular
    - angularjs
    - npm
last_update:
  date: 12/10/2025
  author: Jeyson Andrés García Rodríguez
---

# Modelo

Antes de iniciar con este tutorial vamos a crear un componente nombrado **titulo**. Debemos validar que se crean los archivos **titulo.ts**, **titulo.spec.ts**, **titulo.css** y **titulo.html** dentro de la carpeta **titulo**. 

El modelo de un componente representa las variables necesarias para que ejecute su funcionamiento. Dichas variables se crean dentro de la definición del componente, en nuestro caso **titulo.ts**. 

Vamos a crear dos variables de tipo cadena de texto (**String**). La primera sera nombrada **nombre** y la segunda será nombrada **apellido**. La variable **apellido** permite valores nulos o vacíos. 

![Modelo del componente título](/img/angular-modelo-1.png)

Esto quiere decir que en nuestro HTML (**titulo.html**) podemos usar las variables **nombre** y **apellido**.

![HTML del componente título](/img/angular-modelo-2.png)


