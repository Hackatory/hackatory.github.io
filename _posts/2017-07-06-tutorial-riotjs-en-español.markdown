---
---

Estuvimos usando [RIOT][1] una librería que permite implementar
componentes web de una manera muy simple.

La idea de RIOT es hacer componentes, o sea elementos html nuevos que sirvan
propósitos específicos en las páginas que realizamos, cada componente tiene
html, css y javascript integrados, de forma que se pueden reutilizar en
distintos contextos.

Lo que vamos a hacer en este tutorial es un formulario para escribir comentario
el cual nos va a mostrar en simultaneo una pre-visualización del mismo.

Primero vamos a necesitar incluir el compilador de riot, que como es muy
liviano no es problemático, para eso, necesitamos simplemente agregar un
script:

```html
<script src="https://cdn.jsdelivr.net/npm/riot@3.6/riot+compiler.min.js"></script> 
```

Este script se va a encargar de compilar todos los scripts del tipo:
`riot/tag`, que es el formato en el que escribiremos nuestro componente.

Este archivo es muy fácil de escribir ya que la sintaxis es la misma que en
html, lo que hacemos es indicar como queremos que se vea nuestro componente, el
código lo guardaremos en un archivo `preview-comment.tag` con el siguiente
contenido:

```html
<preview-comment>
  <h3>Nuevo Commentario</h3>

  <form>
    <label>Email
      <input type="email" name="email">
    </label>
    <label>Comentario
      <textarea name="comment"></textarea>
    </label>
    <input type="submit">
  </form>

  <article class='preview comment'>
    <p>{comment}</p>
  </article>
</preview-comment>
```

Para usar el tag en nuestra página, necesitamos, por un lado cargar el código,
por otro lado indicar dónde queremos que aparezca y por último "montarlo".

```html

<!-- cargamos el tag -->
<script type="riot/tag" src="preview-comment.tag"></script>

<!-- indicamos dónde queremos ver el tag -->
<preview-comment>
</preview-comment>

<!-- montamos el componente -->
<script>
  riot.mount('preview-comment')
</script>
```

Con eso debería alcanzar para que veamos el formulario, pero la
previsualización todavía no anda, para hacerlo andar, vamos a necesitar agregar
código javascript en nuestro tag y modificar el campo de comentario, para
poder referenciarlo.

```html
<textarea name="comment" ref='comentario' onKeyPress={cambioComentario}></textarea>

<script>
  this.cambioComentario = function (evt) {
    let nueva_letra = String.fromCharCode(evt.charCode)
    this.comment = this.refs.comentario.value + nueva_letra
  }
</script>
```

De esta manera, cuando el usuario escribe algo en el campo comentario, automaticamente ese cambio se ve reflejado en la pre-visualización.

También podemos mostrar el avatar del usuario de manera automática,
utilizando gravatar, para lo cual necesitaremos agregar una librería javascript:

    <script src="https://cdnjs.cloudflare.com/ajax/libs/blueimp-md5/2.7.0/js/md5.min.js"></script>

Una vez que agregamos esta librería en nuestra página, podemos modificar el
agregar la imagen del avatar con el siguiente código:

    <img src="//www.gravatar.com/avatar/{gravatar_id}.jpg">

    <script>
      this.cambioEmail = function () {
        this.gravatar_id = md5(this.refs.email.value)
      } 
    </script>

De este modo, cuando el usuario ingresa su email, ve su imagen de perfil (si está cargada en gravatar) al lado de su comentario.

Por último, solo resta agregar algunos estilos en nuestro nuevo tag.


```html
<style>
  label, input, textarea {
    display: block;
  }

  .preview {
    background-color: grey;
    width: 300px;
    min-height: 100px;
    border-radius: 15px;
  }

  .preview img {
    margin: 10px;
    border-radius: 50%;
    float: left;
  }
</style>
```

Con este código ya deberíamos tener nuestro primer elemento funcionando.

[1]: http://riotjs.com/
