# Next.js Basics
## Definiciones:
### Client Side Rendering(CSR)
<div style="text-align: justify">

Este tipo de reenderizado se hace mediante páginas de javascript vanilla, aplicaciones de Create React App(CRA) o tabién mediante otros frameworks de javasctipt como Astro o Gatsby.

El usuario hace un request al servidor donde esta almacenada la página, la respuesta es un paquete con todo el javascript, HTML y jsx de la página, el navegador tiene que esperar a la respuesta y luego procesar todo el javascript, paquetes, lógica e interactividad de la página. Una vez procesado todo el javascript y el jsx el navegador reenderiza el resultado del HTML y el js y jsx.

Cuando estamos en un proyecto de React, la respuesta del servidor va a ser una plantilla de HTML con todo lo básico y una etiqueta de body con un id root. En este body se cargará todo el contenido generado por el jsx solamente depués de que el navegador lo procese tras haberlo recibido como parte de la respuesta del servidor. Es por esa razón que el código fuente se encuentra tan vacio, pues, todo el proceso de reenderizado lo esta realizando el navegador en tiempo real mediante el código jsx proporcionado por el servidor. Todo se va a estar procesando y reenderizando desde el navegador o, *"cliente"*.

<br/>
<img src="./assets/CSR_React_Source_Code.png" alt="Source Code of a React CSR Page" style="width: 60%"/>

<br/>

* ### Pros:
* ### Contras:

</div>

## Server Side Rendering(SSR)