# Next.js Basics
## Definiciones:
### __Client Side Rendering(CSR):__
<div style="text-align: justify">

Este tipo de reenderizado se hace mediante páginas de javascript vanilla, aplicaciones de Create React App(CRA) o tabién mediante otros frameworks de javasctipt como Astro o Gatsby.

El usuario hace un request al servidor donde esta almacenada la página, la respuesta es un paquete con todo el javascript, HTML y jsx de la página, el navegador tiene que esperar a la respuesta y luego procesar todo el javascript, paquetes, lógica e interactividad de la página. Una vez procesado todo el javascript y el jsx el navegador reenderiza el resultado del HTML y el js y jsx.

Cuando estamos en un proyecto de React, la respuesta del servidor va a ser una plantilla de HTML con todo lo básico y una etiqueta de body con un id root. En este body se cargará todo el contenido generado por el jsx solamente depués de que el navegador lo procese tras haberlo recibido como parte de la respuesta del servidor. Es por esa razón que el código fuente se encuentra tan vacio, pues, todo el proceso de reenderizado lo esta realizando el navegador en tiempo real mediante el código jsx proporcionado por el servidor. Todo se va a estar procesando y reenderizando desde el navegador o, *"cliente"*.

<br/>
<img src="./assets/CSR_React_Source_Code.png" alt="Source Code of a React CSR Page" style="width: 60%"/>

<br/>

* #### Pros:
* #### Contras:
</div>

### __Server Side Rendering(SSR):__

<div style="text-align: justify">

Este tipo de reenderizado se puede realizar mediante la utilización del framework __Next.js__ o bien,  la función de React:
``` javascript
reactDOMServer.renderToString();
```
Este tipo de reenderizado funciona precompilando la página directamente en el servidor en cuanto el navegador solicita la página. Toda la lógica, javascript, jsx, dependencias y llamadas a apis se quedan en el servidor. Lo que regresa al navegador son links y el HTML de la página precargada en el servidor.

Código fuente de uan página simple de Next:

<img src="./assets/SSR_Next_Code.jpeg" alt="Source Code of a Next SSR Page" style="width: 60%"/>
</div>
</br>

* #### Pros:
* #### Contras:

## Conceptos básicos de Next.js
### Sistema de ficheros:
Las apps generadas con Next tienen el siguiente sistema de ficheros básico:
```
project:
    |-public:
    |-src:
        |-pages:
        |   |-api:
        |   |-_app.js
        |   |-_document.js
        |   |-index.js
        |-styles:
```
* __public:__  
Ahí se guardan todos los assets y recursos del proyecto como bién pueden ser imagenes, links, animaciones o cualquier tipo de asset.
* __src:__  
Se guardan tadas las partes que conforman el programa en su estructura más elemental.
* __pages:__  
Se guardan todas las páginas y links o rutas que componen a la aplicación.
### Routing:
Por defecto Next.js proporciona un sistema de routing muy eficiente e intuitivo. Este consiste en generar la rutas en base al mismo sistema de ficheros de Next, de forma que se parece a como se generan rutas en el sistema operativo mediante la creación de folders y jerarquía dentro de los mismos.

En Next todo el apartado de rutas se maneja desde el folder de *__pages__*, Ahí, cada archivo .js generado representa una ruta cuyo nombre es el mismo que el de su correspondiente archivo. Si se crea un archivo llamado `Home.js`, en cuanto se acceda a la dierección _`/Home`_ el contenido reenderizado en la pantalla cambiará al componente representado en `Home.js`.
#### Rutas Anidadas:
Para crear __rutas anidadas__ es importante saber la función del archivo __`index.js`__. Este archivo representa la dirección default de cada ruta. En el folder de pages el componente que cargará al entrar a la dirección (root) _`/`_ será el que esta establecido en el archivo __`index.js`__. Estos mismos conceptos sobre las rutas aplica de la misma forma para las rutas anidadas. Para crear una ruta anidada solo se tiene que generar un folder dentro de pages. El nombre de la subruta será el mismo que el que el de la carpeta creada. El componente index será el que se muestre por default al entrar a la subruta. Los demás componentes creados se mostrarán de la misma manera al acceder a la ruta: _`/Nombre_de_la_carpeta/Nombre_Componente_dentro_de_carpeta`_.
#### Rutas Dinámicas:
Para crear rutas dinámicas solo se tiene que generar un archivo o una ruta normal cuyo nombre este escrito entre corchetes: [Nombre_de_mi_Carpeta].js. El nombre de la ruta servirá como variable a la hora de acceder a la ruta, osea que no estará atada a un solo nombre.