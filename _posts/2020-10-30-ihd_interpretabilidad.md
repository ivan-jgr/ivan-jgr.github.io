---
layout: post
title:  "Interpretabilidad en modelos convolucionales"
date:   2020-10-30 23:30:34 -0600
categories: interpretabilidad
---

Los detalles de implementación y el código para las visualizaciones lo puede encontrar en [mi GitHub](https://github.com/ivan-jgr/intracraneal-hem-detection) 

# Detección de Hemorragias Intracraneales

La hemorragia en la cabeza (hemorragia intracraneal) es una afección relativamente común que tiene muchas causas que van desde traumatismo, accidente cerebrovascular, aneurisma, malformaciones vasculares, presión arterial alta, drogas ilícitas y trastornos de la coagulación sanguínea. Las consecuencias neurológicas también varían ampliamente según el tamaño, el tipo de hemorragia y la ubicación, desde el dolor de cabeza hasta la muerte. La función del radiólogo es **detectar la hemorragia, caracterizar el subtipo de hemorragia, su tamaño y determinar si la hemorragia podría estar poniendo en peligro áreas críticas del cerebro que podrían requerir cirugía inmediata.**

Si bien todas las hemorragias agudas (es decir, nuevas) parecen densas (es decir, blancas) en la tomografía computarizada (CT), las características de imagen primarias que ayudan a los radiólogos a determinar el subtipo de hemorragia son la ubicación, la forma y la proximidad a otras estructuras

<img src='{{site.baseurl}}/assets/img/ihd/subtypes-of-hemorrhage.png'>

Los pacientes pueden presentar más de un tipo de hemorragia cerebral, que puede aparecer en la misma imagen. Si bien las hemorragias pequeñas son menos mórbidas que las hemorragias grandes típicamente, incluso una hemorragia pequeña puede conducir a la muerte porque es un indicador de otro tipo de anomalía grave (por ejemplo, aneurisma cerebral).

**Fuente**: [RSNA Intracranial Hemorrhage Detection](https://www.kaggle.com/c/rsna-intracranial-hemorrhage-detection/overview/hemorrhage-types)

<hr  style="border-top: 1px solid #000; background: transparent;">

# ¿Podría la inteligencia artificial ser una herramienta para los radiólogos?

La hemorragia intracraneal es un problema de salud grave que a menudo requiere un tratamiento rápido e intensivo. La identificación de cualquier hemorragia presente es un paso crítico en el tratamiento del paciente. Los radiólogos deben revisar rápidamente las imágenes del cráneo del paciente para buscar la presencia, ubicación y tipo de hemorragia.

<figure>
<center>
<img src='{{site.baseurl}}/assets/img/ihd/cnn.png'>
 <figcaption>Resnet34 </figcaption>
 </center>
</figure>

<hr  style="border-top: 1px solid #000; background: transparent;">

## DeconvNet
Paper: [Visualizing and Understanding Convolutional Networks](https://cs.nyu.edu/~fergus/papers/zeilerECCV2014.pdf)

Se puede pensar en una DeconvNet como un modelo que usa los mismos componentes (filtering, pooling) que una ConvNet pero a la inversa, por lo que en lugar de asignar píxeles a las características, hace lo contrario.  Las DeconvNets se propusieron como una forma de realizar un aprendizaje no supervisado pero pueden usarse como una sonda de una ConvNet ya entrenada.

<img src='{{site.baseurl}}/assets/img/ihd/deconv.png' width="500">

<img src='{{site.baseurl}}/assets/img/ihd/deconv_ct.png' width="600">


<hr  style="border-top: 1px solid #000; background: transparent;">


## Grad-Cam
Paper: [Visual Explanations from Deep Networks
via Gradient-based Localization](https://arxiv.org/pdf/1610.02391.pdf)

El Gradient-weighted Class Activation Mapping (Grad-CAM), utiliza los gradientes de cualquier concepto objetivo (por ejemplo, "perro" en una red neuronal) que *fluye* hacia la capa convolucional final para producir un mapa de localización aproximado las regiones importantes de la imagen para predecir el concepto.

<img src='{{site.baseurl}}/assets/img/ihd/grad_cam.jpg'></img>

<img src='{{site.baseurl}}/assets/img/ihd/grad_cam_ct.png' width="300"></img>


<hr  style="border-top: 1px solid #000; background: transparent;">


## Guided BackPropagation

**Idea:** Las neuronas actúan como detectores de características particulares de la imagen.

- Solo nos interesan las características de la imagen que detecta la neurona, no el tipo de cosas que no detecta
- Entonces, al propagar el gradiente, establecemos todos los gradientes negativos en 0

<img src='{{site.baseurl}}/assets/img/ihd/guided_back_prop_ct.png' width="600">


<hr  style="border-top: 1px solid #000; background: transparent;">

## Guided Grad-CAM

Es posible fusionar visualizaciones de gradientes existentes con Grad-CAM para crear visualizaciones de Guided Grad-CAM que son tanto de alta resolución como discriminatorias de clases. Como resultado, las regiones importantes de la imagen que corresponden a cualquier decisión de interés se visualizan con detalles de alta resolución incluso si la imagen contiene evidencia de múltiples conceptos posibles.

<img src='{{site.baseurl}}/assets/img/ihd/grad_cam.png'>

<img src='{{site.baseurl}}/assets/img/ihd/guided_grad_cam_ct.png' width="600">

