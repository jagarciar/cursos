---
id: useQuery
title: useQuery
sidebar_position: 14
author: jeogarod
description: En este tutorial vamos hacer uso del hook useQuery para gestionar los datos asíncronos obtenidos de una API
tags:
  - react
  - reactjs
  - npm
  - vite
  - componente-funcional
  - hooks
  - useRef
last_update:
  date: 06/18/2025
  author: Jeyson Andrés García Rodríguez
---

# useQuery

**useQuery** es un **hook** que nos permite realizar **peticiones de datos asíncronas**, como una llamada a una API, de manera eficiente y con un manejo automático de estados. Además, [**React Query**](/docs/programacion/reactjs/frameworks/react-query.md) se encarga del **cacheo de los datos**, lo que significa que no tendrás que preocuparte por volver a hacer la misma petición si los datos ya están almacenados y siguen siendo válidos.

Vamos a crear la función **fetchCaracters** que se encargue de obtener los personajes de Rick & Morty. Los personajes de Rick and Morty se obtienen al consumir la API **https://rickandmortyapi.com/api/character**. 

```javascript title="fetchCaracters.js"
const fetchCaracters = async () => {
    const response = await fetch(`https://rickandmortyapi.com/api/character`);
    if (!response.ok) {
        throw new Error('Error al obtener los datos del usuario');
    }
    return response.json();
}

export default fetchCaracters;
```

Luego vamos a crear el componente funcional **Characters** que a través del **hook** **useQuery** consume la API llamando a la función **fetchCaracters**. La variable **data** contendrá el resultado del consumo de la API. La variable **isLoading** contendrá la bandera que permite validar si ya fue consumida la API o no. Finalmente, la variable **isError** contendrá el error (en caso de generarse durante el consumo).

```javascript title="Characters.jsx"
import { useQuery } from '@tanstack/react-query';
import {fetchCaracters} from './fetchCharacters';

export const Characters = ({refresh}) => {
    const { data, isLoading, isError } = useQuery({
        queryKey : ['characters'], 
        queryFn: fetchCaracters});

    if (isLoading) {
        return <div>Cargando...</div>;
    }

    if (isError) {
        return <div>Error al cargar los datos del usuario</div>;
    }

    return (
        <select>
            {data.results.map(character => (
                <option key={character.id} value={character.id}>
                    {character.name}
                </option>
            ))}
        </select>
    );
}
```

Finalmente debemos crear el cliente de [**React Query**](/docs/programacion/reactjs/frameworks/react-query.md) en **main.jsx**.

```javascript title="main.jsx"
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import { Characters } from './Characters.jsx'
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

const queryClient = new QueryClient();

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <QueryClientProvider client={queryClient}>
      <Characters />
    </QueryClientProvider>
  </StrictMode>,
)
```

## Revalidación 

La **revalidación** se refiere al proceso de **actualización** de los datos en la caché. Con **React Query**, la **revalidación** es automática y controlada por la biblioteca. Puedes configurar el **tiempo de caducidad** (tiempo máximo que los datos se consideran válidos) para cada consulta y **React Query** se encargará de volver a validar los datos después de que haya transcurrido ese tiempo.

Además del **tiempo de caducidad**, React Query también **actualiza** automáticamente los **datos en caché** cuando se realizan **mutaciones** (operaciones de escritura, como crear, actualizar o eliminar datos). Después de una mutación exitosa, **React Query** invalida automáticamente la caché de las consultas relevantes para garantizar que los datos sean precisos y estén actualizados.

En nuestro ejemplo debemos modificar el componente **Characters** para adicionar el atributo **refetchInterval** en el **hook** **useHook**. Este atributo define cada cuantos segundos se debe actualizar la data. 

```javascript title="Characters.jsx"
const { data, isLoading, isError } = useQuery({
        queryKey : ['characters'], 
        queryFn: fetchCaracters,
        refetchInterval: 5000, // Revalidar cada 5 segundos});
```

Con la **caché** y la **revalidación** inteligente, [**React Query**](/docs/programacion/reactjs/frameworks/react-query.md) *evita realizar peticiones innecesarias al servidor*. Cuando una consulta ya tiene datos en la caché y aún no ha caducado, [**React Query**](/docs/programacion/reactjs/frameworks/react-query.md) devuelve instantáneamente los datos almacenados en lugar de hacer una nueva solicitud. Incluso en situaciones en las que los datos estén caducados, [**React Query**](/docs/programacion/reactjs/frameworks/react-query.md) solo realiza una nueva solicitud cuando el componente que realiza la consulta está montado en la interfaz de usuario.

Si queremos forzar la actualización antes de que caduque el tiempo debemos hacer uso de la función **refetch**. 

En nuestro ejemplo, el componente funcional **Characters** adicionó un botón que ejecuta la función **refetch()** proporcionada por el **hook** **useQuery**. Al oprimir click sobre el botón, se actualizan la data consumiendo nuevamente la API a través de la función **fetchCharacters**. 

```javascript title="Characters.jsx"
import { useQuery } from '@tanstack/react-query';
import { fetchCaracters } from './fetchCharacters';

export const Characters = ({ refresh }) => {
    const { data, isLoading, isError, refetch } = useQuery({
        queryKey: ['characters'],
        queryFn: fetchCaracters,
        refetchInterval: 5000
    });

    if (isLoading) {
        return <div>Cargando...</div>;
    }

    if (isError) {
        return <div>Error al cargar los datos del usuario</div>;
    }

    return (
        <>
            <select>
                {data.results.map(character => (
                    <option key={character.id} value={character.id}>
                        {character.name}
                    </option>
                ))}
            </select>
            <button onClick={() => refetch()}>Actualizar datos</button>
        </>

    );
}
```