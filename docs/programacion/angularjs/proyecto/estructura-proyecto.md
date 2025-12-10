---
id: estructura-proyecto
title: Estructura del proyecto
author: jeogarod
description: En este tutorial vamos a entender qué archivos y carpetas son creados durante la creación de un proyecto AngularJS
sidebar_position: 3
tags:
    - angular
    - angularjs
    - npm
last_update:
  date: 12/10/2025
  author: Jeyson Andrés García Rodríguez
---

# Estructura del proyecto

Después de crear el proyecto podemos acceder a los archivos y carpetas que fueron creados.

![Estructura del proyecto](/img/angular-estructura-1.png)

- La carpeta **node_modules** refiere a los paquetes **npm** del proyecto. 
- La carpeta **public** refiere a los archivos estáticos como las imágenes. 
- La carpeta **src** refiere al código de los **módulos**, **componentes** y **servicios**. 
- Los archivos **package.json** y **package-lock.json** refiere a las dependencias y definición del proyecto. 
- Los archivos **tsconfig.app.json**, **tsconfig.json**, **tsconfig.spec.json** refieren a la configuración **Typescript**. 
- El archivo **angular.json** refiere a la configuración del proyecto. 
- El archivo **README.md** refiere a la documentación del proyecto.

Al expandir la carpeta **src** podemos visualizar:

![Código del proyecto](/img/angular-estructura-2.png)

- El archivo **server.ts** es creado siempre que el proyecto incluya **SSR**. Este refiere a la configuración necesaria para renderizar la página antes de enviarla al navegador. 
- El archivo **main.ts** y **main.server.ts** son el punto de partida de la aplicación. **main.server.ts** esta asociado a la ejecución de **SSR**. 
- El archivo **index.html** es el que embebe todo el proyecto y lo proyecta al navegador web. 
- El archivo **style.css** refiere a los estilos gráficos de la aplicación. 

La carpeta **app** es la que contiene la definición del componente **app**. Al expandirla :

![Código de los componentes](/img/angular-estructura-3.png)

- Los archivos **app.config.ts** y **app.config.server.ts** refieren a la configuración del componente. **app.config.server.ts** esta asociado a la ejecución de **SSR**.
- El archivo **app.ts** refiere al componente. Los componentes siempre vienen con la definición de los estilos (**app.css**) y el HTML (**app.html**). Este archivo se relaciona directamente con **app.spec.ts** para la ejecución de pruebas. 
- Los archivos **app.routes.ts** y **app.routes.server.ts** refieren a la configuración de enrutamiento. **app.routes.server.ts** esta asociado a la ejecución de **SSR**.



