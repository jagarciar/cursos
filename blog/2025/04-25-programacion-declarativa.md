---
slug: programacion-declarativa
title: Programación declarativa
authors: jeogarod
tags: [programacion, declarativa, react, reactjs]
---

# Piensa en la UI

## Determina qué produce un evento

Puedes desencadenar actualizaciones de estado en respuesta a dos tipos de entradas:

- Entradas humanas, como hacer click en un botón, escribir en un campo, navegar a un link.
- Entradas del ordenador, como recibir una respuesta del navegador, que se complete un timeout, una imagen cargando.

## dentifica los diferentes estados visuales de tu componente 

En las ciencias de la computación, tal vez escucharás algo sobre una **máquina de estad** siendo este uno de muchos **estados**. Si trabajas con un diseñador, habrás visto bocetos para diferentes **estados visuales**. React se encuentra en un punto intermedio de diseño y ciencias de la computación, asi que ambas ideas son fuentes de inspiración.

Primero, necesitas visualizar todos los diferentes **estados** de la UI que el usuario pueda ver:

- Vacío: El formulario tiene deshabilitado el botón “Enviar”.
- Escribiendo: El formulario tiene habilitado el botón “Enviar”.
- Enviando: El formulario está completamente deshabilitado. Se muestra un indicador de carga.
- Éxito: El mensaje “Gracias” se muestra en lugar del formulario.
- Error: Igual que el estado de Escribiendo, pero con un mensaje de error extra.

Al igual que un diseñador, querrás “esbozar” o crear “bocetos” para los diferentes estados antes de añadir tu lógica. Por ejemplo, aquí hay un boceto solo para la parte visual del formulario. Este boceto es controlado por una prop llamado status con valor por defecto de 'empty':


```javascript title="/src/Componente.jsx"
export default function Form({
  status = 'empty'
}) {
  if (status === 'success') {
    return <h1>¡Correcto!</h1>
  }
  return (
    <>
      <h2>Cuestionario sobre ciudades</h2>
      <p>
       ¿En qué ciudad hay un cartel que convierte el aire en agua potable?
      </p>
      <form>
        <textarea />
        <br />
        <button>
          Enviar
        </button>
      </form>
    </>
  )
}

```

Es viable declarar variables de estado para actualizar la UI. Para el formulario que vas a desarrollar, necesitarás cambiar el estado en respuesta de diferentes entradas:

- Cambiar la entrada de texto (humano) debería cambiar del estado Vacío al estado Escribiendo o al revés, dependiendo de si la caja de texto está vacía o no.
- Hacer click el el botón Enviar (humano) debería cambiarlo al estado Enviando .
- Una respuesta exitosa de red (ordenador) debería cambiarlo al estado Éxito.
- Una respuesta fallida de red (ordenador) debería cambiarlo al estado Error con el mensaje de error correspondiente.

### Representa el estado de memoria haciendo uso de useState

En ocaciones, necesitarás representar los estados visuales de tu componente en la memoria con **useState**. Consulta más información de **useState** a través del siguiente link: [](../../docs/reactjs/useState)

<!-- truncate -->