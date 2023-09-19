---
title: Nivel de cifrado parcial
description: Nivel de cifrado parcial
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Nivel de cifrado parcial{#partial-encryption-level}

Especifica si se deben cifrar todos los fotogramas o sólo un subconjunto de ellos. Existen tres niveles de cifrado: bajo, medio y alto.

>[!NOTE]
>
>Solo para seguimiento de vídeo en archivos F4V/H.264.

El cifrado parcial está diseñado para proporcionar a los proveedores de contenido granularidad para codificar el contenido en partes. El cifrado de contenido añade sobrecarga de CPU al dispositivo que descifra y visualiza el contenido. Utilice el cifrado parcial para reducir la sobrecarga de CPU y, al mismo tiempo, mantener una protección muy sólida del contenido. Un caso motivador para usar esta función es un solo fragmento de contenido que se pretende que sea reproducible en dispositivos de baja, media y alta potencia.

Debido a la naturaleza de la codificación de vídeo, no es necesario cifrar el 100% del vídeo para que no se pueda reproducir si se roba. El cifrado parcial tiene tres configuraciones, baja, media y alta, y los porcentajes de cifrado asociados dependen de cómo se codifique el vídeo. Debido a esta dependencia de codificación, el porcentaje del contenido cifrado se encuentra dentro de los siguientes intervalos:

* Alto: codifica todas las muestras.
* Medio: codifica un 50 % de los datos objetivo.
* Bajo: codifica un destino del 20 al 30 % de los datos.

Esta configuración se diseñó con la siguiente regla: Cualquier contenido cifrado en el nivel bajo también se cifra en el nivel medio. Esto garantiza que el mismo fragmento de contenido distribuido con cifrado bajo por una parte y distribuido con cifrado medio por otra parte no comprometa la protección del contenido.

Ejemplo de caso de uso: Al reducir el nivel de cifrado, se reduce la sobrecarga de descifrado en el cliente y se mejora el rendimiento de reproducción en los equipos de gama baja.
