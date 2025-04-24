---
slug: programacion-imperativa
title: Programación imperativa
authors: jeogarod
tags: [programacion, imperativa, react, reactjs]
---

Cuando diseñas interacciones con la UI, seguramente pensarás en como la UI cambia en respuesta a las acciones del usuario. Imagina un formulario que permita al usuario enviar una respuesta:

- Cuando escribes algo en el formulario, el botón “Enviar” se habilita.
- Cuando presionas “Enviar”, tanto el formulario como el botón se deshabilitan, y un indicativo de carga aparece.
    - Si la petición es exitosa, el formulario se oculta, y un mensaje “Gracias” aparece.
    - Si la petición falla, un mensaje de error aparece, y el formulario se habilita de nuevo.

En la programación imperativa, lo descrito arriba se corresponde directamente con como
implementas la interacción. Tienes que escribir las instrucciones exactas para manipular la UI dependiendo de lo que acabe de suceder. Esta es otra manera de abordar este concepto: imagina acompañar a alguien en un coche mientras le dices paso a paso que tiene que hacer.

:::tip
 Se llama imperativo por que tienes que “mandar” a cada elemento, desde el indicativo de carga hasta el botón, diciéndole al ordenador cómo tiene que actualizar la UI.
 :::

:::tip
 Manipular la UI de forma imperativa funciona lo suficientemente bien en ejemplos aislados, pero se vuelve mas complicado de manejar de forma exponencial en sistemas complejos. Imagina actualizar una pagina llena de formularios diferentes
 :::
