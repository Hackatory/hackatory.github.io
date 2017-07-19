---
layout: post
title:  "NPM + Webpack + Riotjs"
date:   2017-07-15 09:28:00 -0300
categories: es
comments: true
---

# Configurando Webpack para RiotJS

Primero, vamos a crear una app de node

    mkdir hola-mundo
    cd hola-mundo
    npm init -y

Esto crea el archivo package.json, que guarda la configuración de la app.

A continuación instalamos todas las dependencias que vamos a usar

    npm install webpack webpack-dev-server tag-loader babel-loader babel-core babel-preset-es2015 --save-dev

Y una vez que termine instalamos riot

    npm install riotjs --save

Luego hay que crear el archivo de configuración de webpack.

cat webpack.config.js

~~~ js
const path = require('path');

const config = {
  entry: './index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },

  module: {
    loaders: [
      {
        test: /\.js$/,
        loader: 'babel-loader',
        exclude: '/node_modules/',
        query: {
          presets: ['es2015']
        }
      },
      {
        test: /\.tag$/,
        use: 'tag-loader',
        exclude: '/node_modules/'
      }
    ]
  }
}

module.exports = config;
~~~

En este punto es interezante modificar el script del package.json para tener un
comando para iniciar el servidor de webpack.

~~~ json
"scrpit" : {
  "dev" : "webpack-dev-server"
}
~~~

El archivo de entrada que pusimos para webpack es index.js y tinene que tener:

~~~ js
    var riot = require('riot')
    require('./tags/hola-mundo.tag')

    document.addEventListener('DOMContentLoaded', () =>
      riot.mount('*')
    )
~~~

Por último tenemos que crear el archivo index.html. Dentro del body tenemos que
agregar el script con el bundle de webpack.

~~~ html
<script src="bundle.js" charset="utf-8"></script>
~~~

Tenemos que dejar corriendo el processo que compila los js en una terminal

    $ npm run dev

Este comando recompila bundle.js cada vez que hacemos un cambio y no es
necesario actualizar el browser cada ves que hacemos un cambio.

## Agregando el primer TAG

Vamos a usar el tag que hicimos en el tutorial anterior en tags/hola-mundo.tag

dentro del bodel del archivo index.html tenemos que agregar el tag.

~~~ html
<hola-mundo />
~~~

Podemos copiar el tag muchas veces y por cada una veremos un mensage de "Hola
mundo" en el cliente.
