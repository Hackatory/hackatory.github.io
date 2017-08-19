---
layout: post
title:  "NPM + Webpack"
date:   2017-07-15 09:28:00 -0300
categories: es
comments: true
---

# Qué es Webpack

Webpack en un modulo de node para agrupar multiples archivos, js, css, tags,
ect, en uno o varios archivos que despues pueden compilarse o minificarse para
ser usados en una web. La comunidad de webpack a creado multiples plugins que
pueden ser usados para otorgarles más funcionalidades a webpack, como
actualizar al instante el browser despues de hacer un cambio en el proyecto.

Webpack se hizo particularmente popular con React pero se ha empesado a usar en
otros frameworks como en Ruby on Rails.

# Creando la app de node

Primero, vamos a crear una app de node. Si no tienen node instalado, te
recomiendo usar nvm para esto.

~~~ shell
mkdir webpack-app
cd webpack-app
npm init -y
~~~

Vas a ver una salida como esta:

~~~
{
  "name": "webpack-app",
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

El archivo package.json guarda la configuración de la app. En el futuro cuando
instalemos nuevos módulos, será aquí donde se agregue la dependecia.

## Instalando Webpack

A continuación instalamos webpack, que es una de las depedencias que vamos a usar

~~~ shell
npm install webpack --save-dev
~~~

Tambien podriamos usar la opción -g, pero es mejor instalar la dependencia
dentro del proyecto para tener mejor control de la version que estamos usando.
Si vemos el archivo *package.json*, veremos que se han agregado unas lienas:

~~~ json
  "dependencies": {
    "webpack-dev-server": "^2.7.1"
  }
~~~

tambien se a agregado una carpeta dentro de /node_modules/. La carpeta
/node_modules/ no se recomiendo guardar en el repositorio, no se versiona. Si
otros desarrolladores, se clonan la app, el archivo *package.json* le dice que
modulos debe descargarse usando *npm install*

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

Una funcionalidad muy útil cuando usamos webpack, es que los cambios que
hacemos en los documentos en los que estamos trabajando, se apliquen
instantaneamente en el navegador una vez que salvamos el archivo.

Para esto es necesario instalar un plugin de webpack

~~~shell
npm install html-webpack-plugin --save-dev
~~~

También hay que modificar la configuración de webpack para incluir el uso del plugin.

~~~ shell
cat webpack.config.js
~~~

~~~ js
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

const config = {

  entry: './index.js',

  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },

  plugins: [
    new HtmlWebpackPlugin({
      title: 'Webpack demo'
    })
  ]
}

module.exports = config
~~~

Por último, instalamos webpack-dev-server en la aplication.

~~~ shell
npm install webpack-dev-server --save-dev
~~~

y para iniciar el servidor, simplemente hay que correr:

~~~
webpack-dev-server
~~~
Ahora cada vez que modifiquemos y salvemos alguno de los archivos del proyecto,
deberiamos ver que el browser actualiza inmediatamente. Por ejemplo cambiando
el mensaje en el archivo component.js
