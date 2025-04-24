---
id: crear
title: 2. Creación de un proyecto
author: Jeyson Andrés García Rodríguez
description: Creación de un proyecto y/o aplicativo ReactJS haciendo uso de Vite
sidebar_position: 2
---

# 2. Creación de un proyecto

Basados en las recomendaciones que realizan en diversos sitios web, todos los ejercicios que serán propuestos en este curso se apoyaran de un framework. Los frameworks de **React** resuelven problemas comúnes sin necesidad de realizar trabajos adicionales. Por ejemplo : dan solución a la lentitud de la aplicación, al enrutamiento, entre otras. Es posible que un conjunto de desarrolladores decidan no optar por el uso de un framework a la hora de desarrollar un aplicativo **React**, sin embargo, podrían tomar un poco más de tiempo dando solución a estos inconvenientes que ya fueron solucionados y puestos en una librería adicional (framework).  

Para este caso, nosotros haremos uso de **Vite**. **Vite** es una herramienta para **Frontend** creada por **Evan You** (el mismo creador de **Vuejs**).

La creación de un proyecto u aplicativo **React** haciendo uso de **Vite** se ejecuta a través del siguiente comando:

```javascript
npm create vite@latest
```

Después de ejecutar este comando se debe digitar el nombre del proyecto, seleccionar el framework (**React**) y la variante (**JavaScript + SWC**). **SWC** (**Speedy Web Compiler**) es un compilador de **JavaScript** y que está construido bajo el lenguaje de programación **Rust**. 

Al finalizar la creación debemos realizar la instalación de los paquetes. La instalación de los paquetes se realiza a través del siguiente comando:

```javascript
npm install
```

En caso de querer probar o testear el aplicativo que fue construido por defecto bajo el comando previamente explicado, debemos ejecutar el siguiente comando:

```javascript
npm run dev
```
