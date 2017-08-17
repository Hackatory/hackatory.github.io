---
layout: post
title:  "NPM + Webpack"
date:   2017-07-15 09:28:00 -0300
categories: es
comments: true
---

# Creando la app de node

Primero, vamos a crear una app de node

~~~ shell
mkdir redux-app
cd redux-app
npm init -y
~~~

Vas a ver una salida como esta:

~~~
{
  "name": "redux-app",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
~~~

El archivo package.json guarda la configuración de la app.

## Instalando Webpack

A continuación instalamos todas las dependencias que vamos a usar
~~~ shell
npm install webpack --save-dev
~~~

Tambien podriamos usar la opción -g, pero es mejor instalar la dependencia
dentro del proyecto para tener mejor control de la version que estamos usando.

## Ejecutando Webpack

si en la consola corremose el comando

~~~ shell
webpack
~~~

obtenemos la siguiente salida

~~~
No configuration file found and no output filename configured via CLI option.
A configuration file could be named 'webpack.config.js' in the current directory.
Use --help to display the CLI options.
~~~

## Configuración

Para poder ejecutar webpack, tenemos que crear un archivo de configuración.
creamos el archivo webpack.config.js

~~~
touch webpack.config.js
~~~

Al intentar correr nuevamente webpack vamos a obtener un nuevo error.
Para crear la configuración mínima, necesitamos una entrada(entry) y una salida
(output). la entrada es el primer archivo que incluye a todos los demas y la
salida es el archivo compilado.

~~~ js
const path = require('path');

const config = {
  entry: './index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
}

module.exports = config;
~~~

El archivo de entrada que pusimos para webpack es index.js y tinene que tener:

~~~js
console.log('hola mundo')
~~~

si corremos el comando *webpack* de nuevo, se creará en la carpeta del
proyecto, dentro de la carpeta *dist*, un nuevo archivo, *bundle.js*, que
contiene el javascript compilado.

Pero la verdadera magia ocurre cuando queremos compilar más de un archivo. En
el archivo de entrada, en el index.js, vamos a requerir un segundo archivo y lo
vamos a pegar en el body del documento.

~~~ shell
cat index.js
~~~

~~~ js
import component from './component';

document.body.appendChild(component());
~~~

Y en el archivo *component* ponemos

~~~js
export default (text = 'Hola mundo') => {
  const element = document.createElement('div')

  element.innerHTML = text

  return element

}
~~~

Si creamos un documento de html y agregamos el archivo compilado.

~~~html
<!DOCTYPE html>
<html>
  <head>
    <title>Webpack App</title>
  <body>
    <script type="text/javascript" src="dist/bundle.js"></script>
  </body>
</html>
~~~

Cuando abrimos este documento en un navegador, podemos ver el mensaje "Hola
mundo" que pusimos en el código javascript.

## Cambios instantaneos en el navegador

~~~shell
npm install html-webpack-plugin --save-dev
~~~
