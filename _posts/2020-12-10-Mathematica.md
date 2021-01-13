---
layout: post
title:  "Introducción a Mathematica"
date:   2020-11-21 23:30:34 -0600
categories: dimensionalidad
---

La filosofía de Mathematica es ser tan parecido posible a hacer matemática con papel y lápiz. La característica más importante de Mathematica es que puede realizar álgebra además de aritmética.

## Expresiones Simbólicas
En Mathematica puede evaluar expresiones numéricas pero también simbólicas. Por ejemplo la siguiente expresión
<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/expr.png'>
 </center>
</figure>
asumiento que a `x` no se le ha asignado ningún valor, entonces es guardada en  `y`, no como un número sino como la expresión $$x^2$$. Como `y` es un símbolo puede realizar operaciones que no se pueden con expresiones numéricas, por ejemplo pude derivar `y` i.e. obtener $$\dfrac{dy}{dx}$$
<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/derivative.png'>
 </center>
</figure>
El operador `D` calcula la derivada de `y` con respecto a `x`. Mathematica conoce las reglas de cálculo y puede diferenciar $$x^2$$.

## Celdas
Un notebook está dividido en celdas mostradas por corchetes en el lado derecho del notebook.

**Input Cell** donde puede ingresar expresiones. Para evaluar una celda puede presionar `Shift +  Enter`\\
**Output Cell** muestra resultados.\\
**Group Cell** agrupan celdas de entrada y salida.

### Gráficas

Graficar una función en un rango específico:

<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/plot1.png'>
 </center>
</figure>

Graficar funciones multivariable

<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/plot2.png'>
 </center>
</figure>

Gráfica de una función paramétrica
<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/plot3.png'>
 </center>
</figure>

Gráfica de una superficie paramétrica

<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/plot4.png'>
 </center>
</figure>

### Cálculo

Derivar una función de una variable
<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/plot5.png'>
 </center>
</figure>

Derivar una función multivariable, esta expresión es equivalente a $$\dfrac{\partial^3 f}{\partial^2 x \, \partial y}$$
<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/plot6.png'>
 </center>
</figure>

Calcular el gradiente de una función $$\nabla f(x, y, z)$$
<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/grad.png'>
 </center>
</figure>

Calcular una integral indefinida $$\displaystyle\int (x^2 + \sin x) \, dx$$
<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/plot7.png'>
 </center>
</figure>

Evaluar una integral definida $$\displaystyle \int_0^1 \dfrac{1}{x^3 + 1} \, dx$$
<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/plot8.png'>
 </center>
</figure>

También puede calcular integrales dobles, triples, etc.
<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/plot9.png'>
 </center>
</figure>

### Campos Vectoriales

Graficar un campo vectorial, note que la magnitud de cada vector de muestra en función del color (menor magnitud en azul y mayor en naranja-amarillo)
<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/vector1.png'>
 </center>
</figure>

Para verlo en una escala diferente puede usar la opción `VectorScale -> Automatic`.

<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/vector2.png'>
 </center>
</figure>

Graficar las lineas de flujo o curvas integrales de un campo vectorial.
<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/vector3.png'>
 </center>
</figure>

Calcular la divergencia y rotacional de un campo vectorial.

<figure>
<center>
<img src='{{site.baseurl}}/assets/img/mathematica/div_curl.png'>
 </center>
</figure>