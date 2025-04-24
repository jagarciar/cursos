---
author: "Jeyson Andrés García Rodríguez"
id: componentes-clase
sidebar_position: 5
title: 5. Componentes de clase
---

# 5. Componentes de clase

**React** es una biblioteca de **JavaScript** para renderizar **interfaces de usuario** (**UI** por sus siglas en inglés). La **UI** se construye a partir de pequeñas unidades como botones, texto e imágenes. **React** te permite combinarlas en **componentes reutilizables** y anidables. **React** clasifica los componentes en : **componentes funcionales** y **componentes de clase**.

Los **componentes de clase** son **clases** que extienden de la super clase **React.Component**. Los **componentes de clase** permiten guardar el **estado** y permiten controlar lo que ocurre durante su **ciclo de vida**, exponiéndonos métodos como **componentDidMount** o **componentWillUnmount**. 

A continuación tenemos en un archivo **Componente.jsx** la definición y creación de un componente nombrado **Componente**. Al ser un **componente de clase** y extender de la super clase **React.Component**, **Componente** debe definir las funciones **componentDidMount**, **componentWillUnmount** y **render**. La función **render** representará el retorno **HTML** del **componente**.

```javascript title="/src/Componente.jsx"

import React from 'react'

export class Componente extends React.Component {
    constructor(props){
        super(props)
    }

    componentDidMount(){
        
    }

    componentWillUnmount(){
        
    }

    render(){
        return(
            <p>Hola, soy un componente</p>
        )
    }
}
```

:::warning
En la mayoría de sitios web recomiendan hacer uso de **componentes funcionales** por encima de los **componentes de clase**
:::