---
seo-title: Nivel de cifrado parcial
title: Nivel de cifrado parcial
uuid: 462ca2d0-0d37-43a8-b8a0-8a25ecf73ce1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Nivel de cifrado parcial{#partial-encryption-level}

Especifica si se deben cifrar todos los marcos o solo un subconjunto de marcos. Existen tres niveles de cifrado: baja, media y alta.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Solo para la pista de vídeo en archivos F4V/H.264.

El cifrado parcial está diseñado para proporcionar granularidad a los proveedores de contenido para codificar el contenido en partes. El cifrado de contenido añade una sobrecarga de CPU al dispositivo que descifra y visualiza el contenido. Utilice el cifrado parcial para reducir la sobrecarga de la CPU mientras mantiene una protección muy sólida del contenido. Un caso motivador para utilizar esta función es una sola parte de contenido que se pretende reproducir en dispositivos de baja, media y alta potencia.

Debido a la naturaleza de la codificación de vídeo, no es necesario cifrar el 100 % del vídeo para que no se pueda reproducir si se roba. El cifrado parcial tiene tres configuraciones: baja, media y alta, y los porcentajes asociados de codificación dependen de cómo se codifique el vídeo. Debido a esta dependencia de codificación, el porcentaje del contenido que se cifra se encuentra dentro de los siguientes rangos:

* Alta: Codifica todos los ejemplos.
* Medio: Cifra un 50 % de los datos objetivo.
* Bajo: Codifica un objetivo del 20 al 30 % de los datos.

Esta configuración se diseñó con la siguiente regla: Cualquier contenido cifrado en la configuración baja también se cifra en la configuración media. Esto garantiza que la misma porción de contenido distribuida por una parte con bajo cifrado y distribuida a medio cifrado por otra parte no comprometa la protección del contenido.

Ejemplo de caso de uso: La reducción del nivel de cifrado reduce la sobrecarga de descifrado en el cliente y mejora el rendimiento de reproducción en equipos de gama baja.
