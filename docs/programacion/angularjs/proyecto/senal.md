---
id: senales
title: Señales
author: jeogarod
description: En este tutorial vamos a entender qué es una señal, cómo se crea una señal y para qué y por qué son necesarios en un proyecto en AngularJS
sidebar_position: 7
tags:
    - angular
    - angularjs
    - signal
    - npm
last_update:
  date: 12/10/2025
  author: Jeyson Andrés García Rodríguez
---

# Señales

Una **señal** es un **contenedor** que envuelve un **valor** y **notifica** a los **usuarios interesados cuando este cambia**. Las **señales** pueden contener cualquier valor, desde primitivos hasta estructuras de datos complejas. 

El valor de una **señal** se lee llamando a su función **getter**, lo que le permite a **Angular JS** rastrear donde se utiliza. 

Las **señales** pueden ser de solo lectura o escritura. 

Vamos a crear dentro de un proyecto en **Angular JS** un componente llamado **Contador**. Dentro del componente **Contador** vamos a crear una variable llamada **numero** y un método llamado **incrementar()**. El método **incrementar()** debe sumar el valor de la variable **numero** con 1. La variable **numero** tiene el valor por defecto 0. 

![Componente contador](/img/angular-signal-1.png)

Ahora, en el **HTML** del componente **Contador** vamos a poner en un parráfo el valor de la variable **numero** y a partir de un botón la invocación del método **incrementar()**. 

![HTML del componente contador](/img/angular-signal-2.png)

Si ejecutamos nuestro componente encontraremos un error : "El método **incrementar()** se ejecuta pero no se actualiza el valor de la variable **numero** en el **HTML** de nuestro componente". Para que esto suceda debemos adicionar **signal** a la variable **numero**. 

![Uso de signal en el componente Contador](/img/angular-signal-3.png)

Al convertir la variable **numero** a **signal** debemos hacer uso de los métodos **set** y **get** para actualizar y obtener el valor respectivamente. En este caso, en el método implementar obtuvimos el valor de **numero** a través del método **this.numero()** y la actualizamos después de invocar el método **this.numero.set()**. 

![Uso de signal en el HTML del componente Contador](/img/angular-signal-4.png)

Al convertir la variable **numero** a **signal** debemos modificar el **HTML** del componente para que invoque el método **numero()** para visualizar el valor de la variable.

![Metodo update en el signal](/img/angular-signal-5.png)

Como alternativa podemos hacer uso del método **this.numero.update()** para actualizar el valor de la variable **numero**. 

