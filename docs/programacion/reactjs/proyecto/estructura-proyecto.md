---
id: estructura-proyecto
title: Estructura
description: En este tutorial vamos a descifrar qué carpetas y archivos fueron creados después de la creación de un proyecto ReactJS
sidebar_position: 2
author: jeogarod
tags:
  - react
  - reactjs
  - createRoot
  - npm
  - vite
last_update:
  date: 04/24/2025
  author: Jeyson Andrés García Rodríguez
---

# ¿De qué está compuesto nuestro proyecto ReactJS?

Fue creado previamente un proyecto y/o un aplicativo **ReactJS** haciendo uso de **Vite** como se explicó en el tutorial [2. Creación de un proyecto](/docs/programacion/reactjs/proyecto/crear-proyecto.md).

El resultado obtenido es un conjunto de archivos y carpetas con la siguiente estructura:

```
├── node_modules
├── public
├── src
│   ├── assets
│   ├── App.css
│   ├── App.jsx
│   ├── index.css
│   ├── main.jsx
├── .gitignore
├── eslint.config.js
├── index.html
├── package-lock.json
├── package.json
└── vite.config.js
```

- La carpeta **node_modules** almacena o contiene los paquetes y/o dependencias que son necesarios para la ejecución de nuestro proyecto y/o aplicativo. 
- Los paquetes y/o dependencias que deben ser instalados para el proyecto y/o aplicativo se encuentran enlistados en el archivo **package.json**. 
- El archivo **eslint.config.js** contiene la configuración de **ESLint** para el proyecto y/o aplicativo. **ESLint** es una herramienta de código abierto enfocada en el proceso de **linting** para **Javascript**.
- El archivo **.gitignore** contiene la configuración de cuáles archivos o fuentes serán cargados en el repositorio y cuáles serán excluidos. 
- El archivo **vite.config.js** contiene la configuración de **Vite**. 
- El archivo **index.html** es la raíz de nuestro proyecto y/o aplicativo enlazado con **/src/main.jsx**. El archivo **/src/main.jsx** se encarga de encapsular el **componente funcional** o **componente de clase** principal. Este archivo importa la definición de estilos **CSS** según las reglas descritas en **/src/index.css**. 
- Al crear un proyecto y/o aplicativo en **React** se crea un **componente** nombrado **App** exportado en el archivo **/src/App.jsx**. Este archivo importa la definición de estilos **CSS** según las reglas descritas en **/src/App.css**. 
- La carpeta **public** contendrá todos los archivos de tipo imagen que sean necesarias incluir en nuestro aplicativo y/o proyecto. 
- La carpeta **/src/assets** contendrá todos los archivos de tipo imagen que sean necesarias incluir en los **componentes funcionales** y/o **componentes de clase**.

:::tip
Los **componentes funcionales** y/o **componentes de clase** que sean creados en nuestro aplicativo y/o proyecto en **React** deben ser alojados bajo la carpeta **/src**. 
:::
