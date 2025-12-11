---
id: servicios
title: Servicios
author: jeogarod
description: En este tutorial vamos a entender qué son los servicios y como se integran con un componente
sidebar_position: 11
tags:
    - angular
    - angularjs
    - npm
last_update:
  date: 12/10/2025
  author: Jeyson Andrés García Rodríguez
---

# Servicios

Los **servicios** son piezas reusables de código que pueden ser inyectadas. 

Los servicios deben ser creados bajo el comando **ng generate service name** donde **name** es el nombre del servicio. En el siguiente ejemplo vamos a crear un servicio llamado Incrementar. 

![Creación de un servicio](/img/angular-servicios-1.png)

Al finalizar la creación se puede observar que se adicionaron dos documentos en la carpeta **app** : **incrementar.ts** y **incrementar.spec.ts**. 

![Archivos creados](/img/angular-servicios-2.png)

**Incrementar** hace uso de **@Injectable()** para definirse como **servicio**. El valor de **provideIn** normalmente es **root** para que cualquier componente pueda hacer uso del servicio. 

![Archivos creados](/img/angular-servicios-3.png)

Dentro del servicio **Incrementar** vamos a definir un método **sumar(x : number, y :number)** que recibe dos parámetros númericos : **x** & **y**. El método retorna el valor de la suma de estos dos parámetros. 

Supongamos que desde el componente **Contador** necesitamos hacer uso del **servicio** **Incrementar**. El componente **Contador** tiene una **señal** **numero** y tiene una inyección del servicio **Incrementar**.  Además tiene un método **incrementar()** el cuál llama al método **sumar** del servicio **Incrementar**. 

![Llamado a los servicios](/img/angular-servicios-4.png)