---
id: condicionales
title: Condicionales
author: jeogarod
description: En este tutorial vamos a entender cómo se puede visualizar un u otro elemento HTML según una variable
sidebar_position: 8
tags:
    - angular
    - angularjs
    - npm
last_update:
  date: 12/10/2025
  author: Jeyson Andrés García Rodríguez
---

# Condicionales

Los condicionales **@if @else** permiten bifurcar la visualización, es decir, según una condición, si es **true** mostrará unos elementos HTML posiblemente diferentes a si es **false**. 

Supongamos que tenemos un componente nombrado **Contador** el cuál tiene una variable **numero** y un método **incrementar()** el cuál suma el valor de la variable **numero** con 1. 

En el **HTML** del componente podemos bifurcar la visualización con una condición como se muestra a continuación:

![Condicionales en angular](/img/angular-condicionales-1.png)

En el ejemplo anterior, siempre que el valor de la variable **numero** sea menor o igual que 5, se mostrará el botón que incrementa el valor de la misma. Si el valor de la variable **numero** es superior a 5, mostrará un parráfo informando que no puede incrementarse. 