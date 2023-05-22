---
description: El formato Audio Codec 3 (AC-3, también conocido como Dolby Digital®) 5.1, permite a los proveedores de contenido comprimir el tamaño de archivos de audio multicanal sin afectar la calidad del sonido. AC-3 es un formato 5.1, lo que significa que proporciona cinco canales de ancho de banda completo para una mejor experiencia de usuario.
title: Formato AC-3 5.1
exl-id: 13f6f7f5-d2d3-4ee2-b2b1-acb199f835ce
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Formato AC-3 5.1 {#ac-format}

El formato Audio Codec 3 (AC-3, también conocido como Dolby Digital®) 5.1, permite a los proveedores de contenido comprimir el tamaño de archivos de audio multicanal sin afectar la calidad del sonido. AC-3 es un formato 5.1, lo que significa que proporciona cinco canales de ancho de banda completo para una mejor experiencia de usuario.

Para obtener más información, consulte [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

TVSDK admite las siguientes funciones de AC-3 5.1:

* Audio envolvente AC-3
* Flujos mixtos/no mixtos para el tipo de audio envolvente
* Posibilidad de consultar el dispositivo para ver si el códec de audio envolvente está disponible en el dispositivo.

   Los resultados determinan qué tipo de códec de audio preferido se selecciona. Se descarta el manifiesto del tipo de códec de audio que el dispositivo no va a utilizar. Por ejemplo, si se ha seleccionado el formato AC-3, no se tienen en cuenta los perfiles con el formato Advanced Audio Coding (AAC).
* Modo de paso a través

   En el modo de paso a través, en lugar de descodificar los medios del formato AC-3 5.1 a un formato de modulación de código de pulso multicanal (PCM), el TVSDK se modifica o no modifica (según el dispositivo) los medios Dolby del Decodificador. Este medio se envía al dispositivo de audio (altavoz o receptor) para que el dispositivo de audio pueda descodificar y reproducir el flujo Dolby surround.

>[!IMPORTANT]
>
>TVSDK admite las funciones AC-3 5.1 solo en el dispositivo Amazon Fire TV de primera generación.

No se admiten las siguientes funciones de AC-3 5.1:

* Audio AAC multicanal
* ABR en diferentes códecs (AAC - AC3)

## Seleccionar medios admitidos {#section_0D7E717BE18B418D817EE017EF2375D1}

Este es el flujo de trabajo típico que se produce cuando TVSDK encuentra un manifiesto con medios AC-3 y AAC:

1. TVSDK consulta qué códec admite el dispositivo.
1. Se selecciona el códec con la calidad más alta.

   Este es el orden en que se selecciona la calidad:

   1. AC-3
   1. AAC

1. TVSDK ignora los perfiles con otros tipos de códec de audio.

>[!TIP]
>
>La aplicación no puede obtener información sobre perfiles ignorados.

## Determinar el modo de salida {#section_D2AFBF33D3904AC2A7C653A60C3A0CD3}

Al procesar medios AC-3, si un dispositivo Android está conectado al sistema de altavoces, la decisión de reproducir contenido en modo surround o estéreo depende de cómo esté configurado el dispositivo.

|  | **Sonido envolvente** | **Altavoz estéreo** |
|---|---|---|
| Configuración del dispositivo Dolby activado (o automático) | Configuración del dispositivo Dolby activado (o automático) | Modo estéreo |
| Configuración del dispositivo Dolby desactivado | Modo estéreo | Modo estéreo |
