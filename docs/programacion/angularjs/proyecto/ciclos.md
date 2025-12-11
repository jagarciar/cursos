---
id: ciclos
title: Ciclos
author: jeogarod
description: En este tutorial vamos a entender cómo se puede iterar un conjunto de variables
sidebar_position: 9
tags:
    - angular
    - angularjs
    - npm
last_update:
  date: 12/10/2025
  author: Jeyson Andrés García Rodríguez
---

# Ciclos

El ciclo **@for** permite iterar un conjunto de valores. 

Supongamos que tenemos un componente nombrado **Contador** el cuál tiene una variable **numero** y un método **incrementar()** el cuál suma el valor de la variable **numero** con 1. 

El componente **Contador** tiene también una variable **numeros** la cuál almacena todos los valores que se han incrementado. Esto lo realiza en cada llamado al método **incrementar**.

![Array de numeros](/img/angular-ciclos-1.png)

En el **HTML** del componente podemos iterar los valores del arreglo de números. 

![Iteración en HTML](/img/angular-ciclos-2.png)