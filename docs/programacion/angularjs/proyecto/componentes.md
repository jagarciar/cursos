---
id: componentes
title: Componentes
author: jeogarod
description: En este tutorial vamos a entender qué es un componente, cómo se crea un componente y para qué y por qué son necesarios en un proyecto en AngularJS
sidebar_position: 4
tags:
    - angular
    - angularjs
    - npm
last_update:
  date: 12/10/2025
  author: Jeyson Andrés García Rodríguez
---

# Componentes

## ¿Qué son?

Los **componentes** son el bloque de código principal en un proyecto de **AngularJS**. Cada **componente** representa una parte de una página web más grande. Organizar el proyecto en **componentes** ayuda a estructurar el proyecto, separando claramente el código en partes especificas que son fáciles de mantener y ampliar con el tiempo. 

## ¿Cómo se crean?

Ubicados dentro del proyecto **AngularJS** debemos ejecutar el comando **ng**:

```javascript
ng generate componente component
```

![Creación del proyecto](/img/angular-creacion-componente-1.png)

En dado caso pregunte si se desea compartir estadisticas con Google pueden aceptar o rechazar sin problema. En mi caso, yo acepté. 

Después de crear el componente podremos observar que dentro de la carpeta **app** se creó la carpeta del componente. Dicha carpeta contiene la definición de los estilos gráficos (**.css**) y del HTML (**.html**) del componente (**.ts**) junto a la definición de las pruebas (**spec.ts**).

![Creación del proyecto](/img/angular-creacion-componente-2.png)

En nuestro ejemplo creamos el componente **titulo**.

![Componente titulo](/img/angular-creacion-componente-3.png)

Todos los componentes tienen inyectada la dependencia **@Component**. Esta inyección refiere a la definición de estilos gráficos (**styleUrl**), del HTML (**templateUrl**) y al nombre del selector (**selector**). 

## ¿Cómo se integran?

En las secciones previas creamos un componente nombrado **titulo**. Al ser un componente (**titulo.ts**) tenemos la definición de los estilos gráficos (**titulo.css**), el HTML (**titulo.html**). 

El HTML del componente título es el siguiente:

![HTML del componente título](/img/angular-creacion-componente-4.png)

Vamos a importar el componente **titulo** en el componente principal **app**. 

1. Debemos ir a la definición del componente **app.ts** e importar el componente **titulo**. 

![Importar componente](/img/angular-creacion-componente-5.png)

2. Debemos ir al HTML del componente **app.html** y adicionar donde sea necesario el selector del componente **titulo** (el cuál se definió en **titulo.ts**).

![Incluir selector](/img/angular-creacion-componente-6.png)

Finalmente podemos visualizar la adición

![Importación finalizada](/img/angular-creacion-componente-7.png)

:::tip 
Ten en cuenta que debes importar el componente en la definición del otro (en el ejemplo la importación de **Titulo** dentro de **app.ts**). Si no se hace esto, se va generar la siguiente excepción:

is a Web Component then add 'CUSTOM_ELEMENTS_SCHEMA' to the '@Component.schemas' of this component to suppress this message
:::

