---
layout: page
title: Hackatory
permalink: /about/
---

## Donde está?

Av. Gdor. Freire 3043 departamento 4, es al lado de Santa Lucía (mapa). El timbre se escucha muy bajo, así que acerquen la oreja al auricular.

<iframe width="425" height="350" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" src="https://www.openstreetmap.org/export/embed.html?bbox=-60.71830809116364%2C-31.638982430060494%2C-60.71468710899353%2C-31.637370227730322&amp;layer=mapnik&amp;marker=-31.63817633238918%2C-60.71649760007858" style="border: 1px solid black"></iframe>
<br/>
<small><a href="http://www.openstreetmap.org/?mlat=-31.63818&amp;mlon=-60.71650#map=19/-31.63818/-60.71650">Ver mapa en pantalla completa</a></small>

## Cuanto cobramos

No cobramos nada. El que quiere poner plata o tiempo para lo que se necesite, está invitado a hacerlo.

## WiFi

Hay wifi en la oficina, la red se llama `hackerlab` y la password es `aprenderaprogramar`.

## Cómo nos organizamos

Hasta ahora, la única cuestión es intentar limpiar y ordenar un poco los jueves por la tarde y sacar la basura al salir el viernes.

Para gestionar los gastos, lo que hacemos es cargar los gastos en un google form.

## Quienés somos

<div class="hackers">
  {% for hacker in site.hackers %}
    {% if hacker.show %}
      {% include hacker_profile.html %}
    {% endif %}
  {% endfor %}
</div>

