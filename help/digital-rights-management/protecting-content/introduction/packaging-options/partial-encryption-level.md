---
title: Nivel de cifrado parcial
description: Nivel de cifrado parcial
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Nivel de cifrado parcial {#partial-encryption-level}

Esta opción de empaquetado especifica si se deben cifrar todas las tramas o solo un subconjunto de tramas. Hay tres niveles de encriptación: baja, media y alta.

>[!NOTE]
>
>El cifrado parcial se aplica solo a la pista de vídeo en archivos F4V/MP4.

El cifrado parcial está diseñado para proporcionar granularidad a los proveedores de contenido para codificar el contenido en partes. El cifrado de contenido añade una sobrecarga de CPU al dispositivo que está descifrando y viendo el contenido. Utilice el cifrado parcial para reducir la sobrecarga de CPU mientras mantiene una protección muy sólida del contenido. Un caso motivador para utilizar esta función es una única pieza de contenido que se pretende reproducir en dispositivos de baja, media y alta potencia.

Debido a la naturaleza de la codificación de vídeo, no es necesario cifrar el 100 % del vídeo para que no se pueda reproducir si se roba. El cifrado parcial tiene tres configuraciones: baja, media y alta, y los porcentajes de cifrado asociados dependen de cómo se codifique el vídeo. Debido a esta dependencia de codificación, el porcentaje del contenido cifrado se encuentra dentro de los siguientes intervalos:

* Alto: Codifica todas las muestras.
* Medio: Codifica un destinatario el 50 % de los datos.
* Bajo: Codifica un objetivo del 20 al 30 % de los datos.

Estos ajustes se diseñaron con la siguiente regla: Cualquier contenido cifrado en la configuración baja también se cifra en la configuración media. Esto garantiza que el mismo fragmento de contenido distribuido con un cifrado bajo por una parte y distribuido a medio cifrado por otra parte no comprometa la protección del contenido.

Ejemplo de caso de uso: Al reducir el nivel de encriptación, disminuye la sobrecarga de descifrado en el cliente y mejora el rendimiento de reproducción en equipos de gama baja.
