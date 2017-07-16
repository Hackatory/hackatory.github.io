---
layout: post
title:  "Riot Tutorial 1 - Componente Básico"
date:   2017-07-14 10:00:00 -0300
tags: tutorial
categories: en
comments: true
---

En este tutorial vamos a crear un componente o etiqueta personalizada utilizando [riot.js](http://riotjs.com/){:target="_blank"} el cuál mostrará un mensaje de saludo con un nombre previamente establecido, o con la palabra "mundo" sino se suministra ningún nombre.

## **Componente**
Los componentes **pueden incluír** tres secciones:
1. ***CSS*** (estilos del componente).
2. ***HTML***. 
3. ***Javascript*** (comportamiento deseado).


```
<!-- hello-world.tag -->
<hello-world>
  <style>
    h1 { color: red; }
  </style>

  <h1>hola {name}!</h1>

  <script>
    this.name = opts.name 
  </script>
</hello-world>
```
En el script de arriba ```opts.name``` contiene el valor del ```name``` proveniente del archivo HTML. Ese valor es el que será mostrado en el encabezado h1.  

## **Archivo HTML**  
```
<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
  <title>Riotjs - Tutorial 1</title>
  <script type=riot/tag src="hello-world.tag"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/riot/3.6.1/riot+compiler.min.js"></script>
  <script>
    // El saludo por defecto será "hola mundo!"
    riot.mount('hello-world', {name: 'mundo'})
  </script>
</head>

<body>
  <!-- Saludos personalizados -->
  <hello-world name="Lucas"/>
  <hello-world name="Pablo"/> 
  <!-- Saludo por defecto -->
  <hello-world/>
</body>
</html> 
```
Notar que las etiquetas del componente ```<hello-world/>``` que definimos se cierran a si mismas. Riot soporta self-closing así que no es necesario colorcar ```<hello-world></hello-world>```.
