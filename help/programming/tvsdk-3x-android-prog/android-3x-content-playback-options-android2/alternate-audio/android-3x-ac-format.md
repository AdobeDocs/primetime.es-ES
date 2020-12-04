---
description: El formato de códec de audio 3 (AC-3, también conocido como Dolby Digital®) 5.1, permite a los proveedores de contenido comprimir el tamaño de los archivos de audio multicanal sin perjudicar la calidad de sonido. AC-3 es un formato 5.1, lo que significa que proporciona cinco canales de ancho de banda completo para una experiencia de usuario más rica.
seo-description: El formato de códec de audio 3 (AC-3, también conocido como Dolby Digital®) 5.1, permite a los proveedores de contenido comprimir el tamaño de los archivos de audio multicanal sin perjudicar la calidad de sonido. AC-3 es un formato 5.1, lo que significa que proporciona cinco canales de ancho de banda completo para una experiencia de usuario más rica.
seo-title: Formato AC-3 5.1
title: Formato AC-3 5.1
uuid: 9d1adf33-4c9b-4d31-8212-ac301f3e44c5
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Formato AC-3 5.1 {#ac-format}

El formato de códec de audio 3 (AC-3, también conocido como Dolby Digital®) 5.1, permite a los proveedores de contenido comprimir el tamaño de los archivos de audio multicanal sin perjudicar la calidad de sonido. AC-3 es un formato 5.1, lo que significa que proporciona cinco canales de ancho de banda completo para una experiencia de usuario más rica.

Para obtener más información, consulte [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

TVSDK admite las siguientes funciones AC-3 5.1:

* Audio envolvente AC-3
* Flujos mixtos/no mezclados para el tipo de audio envolvente
* Posibilidad de consulta del dispositivo para ver si el códec de audio envolvente está disponible en el dispositivo.

   Los resultados determinan qué tipo de códec de audio preferido se selecciona. Se descarta el manifiesto con el tipo de códec de audio que el dispositivo no va a usar. Por ejemplo, si se ha seleccionado el formato AC-3, no se tendrán en cuenta los perfiles con el formato de codificación de audio avanzada (AAC).
* Modo de paso

   En el modo de paso, en lugar de descodificar los medios del formato AC-3 5.1 a un formato de modulación de código de impulso multicanal (PCM), el TVSDK se modifica o no se modifica (según el dispositivo) del medio Dolby desde el Decoder. Este medio se envía al dispositivo de audio (altavoz o receptor) para que el dispositivo de audio pueda descodificar y reproducir el flujo envolvente Dolby.

>[!IMPORTANT]
>
>TVSDK admite las funciones AC-3 5.1 solo en el dispositivo Amazon Fire TV de primera generación.

No se admiten las siguientes funciones de AC-3 5.1:

* Audio AAC multicanal
* ABR en diferentes códecs (AAC - AC3)

## Seleccionar medios admitidos {#section_0D7E717BE18B418D817EE017EF2375D1}

Este es el flujo de trabajo típico que se produce cuando TVSDK encuentra un manifiesto con medios AC-3 y AAC:

1. Consultas TVSDK que admiten el códec del dispositivo.
1. Se selecciona el códec con mayor calidad.

   Este es el orden en el que se selecciona la calidad:

   1. AC-3
   1. AAC

1. TVSDK ignora los perfiles con otros tipos de códec de audio.

>[!TIP]
>
>La aplicación no puede obtener información sobre perfiles ignorados.

## Determinar el modo de salida {#section_D2AFBF33D3904AC2A7C653A60C3A0CD3}

Durante el procesamiento de medios AC-3, si un dispositivo Android está conectado al sistema de altavoces, la decisión de reproducir contenido en modo envolvente o estéreo depende de cómo se configure el dispositivo.

|  | **Sonido envolvente** | **Altavoz estéreo** |
|---|---|---|
| Configuración de dispositivo Dolby activado (o automático) | Configuración de dispositivo Dolby activado (o automático) | Modo estéreo |
| Configuración del dispositivo Dolby desactivado | Modo estéreo | Modo estéreo |