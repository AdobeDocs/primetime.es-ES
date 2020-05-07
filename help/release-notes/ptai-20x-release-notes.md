---
title: Notas de la versión de PTAI 20.5.1
description: Las notas de la versión de PTAI 20.5.1 describen las novedades o los cambios que se han producido en la inserción de publicidad dinámica de Primetime en el año 2020.
translation-type: tm+mt
source-git-commit: 9c117678a049e34bfcf960e992a4ce7361968f3e
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Notas de la versión 20.5.1 de Primetime Dynamic Ad Insertion

Las notas de la versión de Inserción de publicidad dinámica 20.5.1 describen las novedades o los cambios, los problemas resueltos y los problemas conocidos en la inserción de publicidad dinámica de Primetime en el año 2020.

## Novedades de PTAI 20.5.1

**Cuando:** Martes 5 de mayo de 2020, de las 4:00 a las 5:00 AM hora del Este

* Se ha corregido un problema para garantizar que se proporcionen encabezados CORS correctos al enviar encabezados If-Modified-Since.

* Corrección de errores en el panel CRS.

* Actualizaciones de mantenimiento.

## Qué ha cambiado en versiones anteriores

### Versión 20.3.4

**Cuando:** Miércoles 1 de abril de 2020, de 03:00 AM a 04:00 AM Hora del Este

* Se ha corregido un problema que provocaba que los subtítulos no estuvieran sincronizados tras la inserción de anuncios en VOD/ WebVTT.

* Actualizaciones de seguridad.

### Versión 20.3.3

**Cuando:** Jueves 26 de marzo de 2020 de las 3:00 a las 4:00 AM Hora del Este

* Las respuestas de SSAI 4XX y 5XX ahora proporcionan correctamente encabezados relacionados con CORS, lo que permite a los clientes de javascript/webview entre dominios leer correctamente las respuestas de error.

* Se corrigió un problema con los encabezados X-Forwarded-For, donde las direcciones IPv6 no se codificaban correctamente en la dirección URL cuando se pasaban a los servidores de publicidad.

* Se corrigió un problema con los flujos de audio CMAF/desmuestreados, en el cual en determinados escenarios los números EXT-X-MEDIA-SEQUENCE se incrementaban incorrectamente.

### Versión 20.3.2

**Cuando:** Miércoles 11 de marzo de 2020 de las 5:30 a las 7:00 AM hora del Este

* Mejoras en la gestión de señales SCTE35.

* Actualizaciones de mantenimiento.

### Versión 20.3.1

**Cuando:** Jueves 5 de marzo de 2020 de las 02:30 a las 04:30 AM hora del Este

* Mejoras de rendimiento:

   * Se Añadió la compatibilidad de caché para los manifiestos m3u8 maestro/medio. Estos manifiestos ahora responden a Cache-Control: los encabezados public y Max-Age, que a menudo pueden mejorar el rendimiento del inicio de vídeo.

   * Se ha Añadido la compatibilidad para forzar la captura de elementos creativos https mediante http, lo que también puede mejorar el rendimiento del inicio de vídeo.

* Correcciones de seguridad y mantenimiento.

### Versión 20.2.1

**Cuando:** Jueves 13 de febrero de 2020 de las 4:30 a las 5:30 AM hora del Este

* Se ha Añadido la compatibilidad con la vinculación de recursos de publicidad que contienen varios flujos de solo audio en función del idioma, el códec o la velocidad de bits.
* Pequeñas mejoras de rendimiento y actualizaciones de mantenimiento.

### Versión 20.1.3

**Cuando:** Martes 28 de enero de 2020 de las 2:00 a las 03:00 AM hora del Este

* **VMAP con compatibilidad FER para nbc CueFormat**

   Convertir señales del flujo FER en parámetros de anulación de línea de tiempo FW, cuando `ptcueformat=nbc` se utiliza y el flujo es un flujo VOD con señales en manifiesto y anuncios integrados.

* Sanice el campo user-agent en el encabezado HTTP antes de reenviarlo a proveedores de publicidad de terceros/CDN.

* Filtre los caracteres de control/no imprimibles (código ASCII &lt; 32) de los encabezados HTTP de usuario-agente antes de enviarlos a Auditude y otros proveedores de publicidad, CDN. Auditude Ad-Call solía fallar para encabezados no válidos.

* Purgue los objetos V1 antiguos de los grupos de NetStorage para mantener el recuento de objetos dentro de los límites seguros de Akamai.

### Versión 20.1.2 [Revisión]

**Cuando:** Lunes 20 de enero de 2020 de las 02:00 a las 03:00 AM hora del Este

* Actualizaciones de mantenimiento.

### Versión 20.1.1

**Cuando:** Miércoles 15 de enero de 2020 de las 4:00 a las 5:00 AM Hora del Este

* El servicio de reempaquetado creativo ahora ofrece una inserción de anuncios más rápida al poner en la lista negra automáticamente los elementos creativos malformados.

* Se Añadió la compatibilidad de la fase 1 con el nuevo formato de señal SCTE 35 en la inserción de anuncios en el servidor.

* Actualizaciones de mantenimiento.

## Problemas resueltos

Cuando la resolución está asociada a un problema informado, se muestra una referencia de Zendesk. Por ejemplo, ZD#xxxxx.

**PTAI 20.5.1**

* Problemas con los encabezados CORS cuando se envían los encabezados If-Modified-Since.

* Problemas en el panel de CRS.

**PTAI 20.3.4**

* Problema que causaba que los subtítulos no estuvieran sincronizados después de insertarlos en VOD/ WebVTT.

**PTAI 20.3.3**

* Problema con los encabezados X-Forwarded-For, donde las direcciones IPv6 no se codificaban correctamente en la dirección URL cuando se pasaban a los servidores de publicidad.

* Problema con los flujos de audio CMAF/desmuestreados, donde en determinados escenarios los números EXT-X-MEDIA-SEQUENCE aumentan incorrectamente en determinados escenarios

## Problemas y limitaciones conocidos

**PTAI 20.3.3**

No se ha agregado ninguna nueva limitación.
