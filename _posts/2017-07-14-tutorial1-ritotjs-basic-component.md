---
layout: post
title:  "Riot Tutorial 1 - Componente Básico"
date:   2017-07-14 10:00:00 -0300
tags: tutorial
categories: es
comments: true
---

En este tutorial vamos a crear un componente o etiqueta personalizada
utilizando [riot.js](http://riotjs.com/){:target="\_blank"} el cuál mostrará un
mensaje de saludo con un nombre previamente establecido, o con la palabra
"mundo" sino se suministra ningún nombre.

## Componente
Los componentes **pueden incluír** tres secciones:
1. **CSS** (estilos del componente).
2. **HTML**.
3. **Javascript** (comportamiento deseado).


```html
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

```opts``` es un objeto que guarda todos los atributos definidos en la etiqueta
de html. En el script de arriba ```opts.name``` contiene el valor del ```name```
proveniente del archivo HTML. Ese valor es el que será mostrado en el
encabezado h1. 

## Archivo HTML

En el head del html cargamos el archivo (.tag) del componente:
```html
<head>
  <script type=riot/tag src="hello-world.tag"></script>
</head>
```
<br>Luego agregamos la biblioteca de riot:
```html
<head>
  <script type=riot/tag src="hello-world.tag"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/riot/3.6.1/riot+compiler.min.js"></script>
</head>
```
<br>Por último montamos el componente:
```html
<head>
  <script type=riot/tag src="hello-world.tag"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/riot/3.6.1/riot+compiler.min.js"></script>
  <script>
     // El saludo por defecto será "hola mundo!"
     riot.mount('hello-world', {name: 'mundo'})
  </script>
</head>
```
<br>El script del componente **hello-world** también se puede escribir así:

```js
this.name = opts.name || "mundo"
```

Esto hace más fácil montar el componente, sin embargo el mensaje por defecto quedaría "adherido" al mismo. En cambio si le pasamos el nombre por defecto al momento de montarlo (como se ve arriba) podremos reutilizar el componente con diferentes nombres por defecto si lo deseamos.

El archivo html terminado debería verse similar al de abajo:

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
  <title>Riotjs - Tutorial 1</title>
</head>

<body>
  <!-- Saludos personalizados -->
  <hello-world name="Lucas"></hello-world>
  <hello-world name="Pablo"></hello-world>
  <!-- Saludo por defecto -->
  <hello-world></hello-world>

  <!-- El script va al final del documento -->
  <script type=riot/tag src="hello-world.tag"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/riot/3.6.1/riot+compiler.min.js"></script>
  <script>
    // El saludo por defecto será "hola mundo!"
    riot.mount('hello-world', {name: 'mundo'})
  </script>
</body>
</html>

```

De esta forma, usamos 3 veces la etiqueta. Las dos primeras, se usan definiendo
un nombre y la tercera usa el valor por defecto.
