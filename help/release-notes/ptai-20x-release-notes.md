---
title: Notas de la versión de PTAI 20.12.1
description: Las notas de la versión de PTAI describen las novedades o los cambios, los problemas resueltos y conocidos en Primetime Ad Insertion en el año 2020.
exl-id: 47e36e42-b6a0-408c-93da-f63c929396b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 0%

---

# Notas de la versión de Primetime Ad Insertion 20.12.1

Las notas de la versión 20.12.1 de Primetime Ad Insertion describen las novedades o los cambios, los problemas resueltos y los problemas conocidos de Primetime Ad Insertion en el año 2020.

## Novedades de PTAI 20.12.1

**Cuándo:** Martes, 08 de diciembre de 2020 de 01:00 a.m. a 04:00 a.m., hora del este

**Cambios**

* Incluye una revisión para solucionar los problemas intermitentes de conectividad de cliente (5xx) en el Ad Insertion de Primetime que se encontraron el 30 de noviembre de 2020.

## Mejoras y correcciones en versiones anteriores de

### Versión 20.11.1

**Cuándo:** Jueves, 5 de noviembre de 2020 de 2:00 a.m. a 05:00 a.m., hora del este

**Cambios**

* Actualizaciones de mantenimiento.

### Versión 20.10.2

**Cuándo:** Jueves, 29 de octubre de 2020 de 12:01 a 06:00 h, hora del este

**Cambios**

* Actualizaciones de mantenimiento.

### Versión 20.10.1

**Cuándo:** Martes, 13 de octubre de 2020 de 03:00 a.m. a 07:00 a.m. hora del este

**Cambios**

* Actualizaciones de mantenimiento.

### Versión 20.9.3

**Cuándo:** Miércoles, 30 de septiembre de 2020 a las 3:30 a. m. a 6:30 a. m. hora del este

**Cambios**

* Se ha añadido el parámetro API de Bootstrap `ptparallelstream`. Esto permite a los clientes con reproductores que solicitan flujos de audio o vídeo demuxados CMAF en paralelo garantizar que los anuncios en las pistas de audio y vídeo sean coherentes. Establezca el valor del parámetro en true para habilitar esta función u omita la deshabilitación.

### Versión 20.9.2

**Cuándo:** Martes, 15 de septiembre de 2020 de 3:30 a.m. a 6:30 a.m., hora del este

**Mejoras**

* Se ha proporcionado compatibilidad con la inclusión de tipos de anuncios no lineales mediante `EXT-X-MARKER` etiquetas.
Para obtener más información o habilitar esta función, póngase en contacto con el representante de soporte técnico.

* Se proporciona compatibilidad para limitar el tiempo total de resolución de anuncios, si los proveedores tardan demasiado en responder. Para habilitar la limitación, establezca el parámetro de API de arranque `ptadtimeout` a un valor en milisegundos.

   >[!NOTE]
   >
   >Este tiempo de espera solo se aplica a solicitudes de publicidad, no a solicitudes de creatividad publicitaria.

### Versión 20.9.1

**Cuándo:** Martes, 1 de septiembre de 2020 de 3:30 a.m. a 7:30 a.m., hora del este

**Cambios**

* Se ha corregido el problema para los clientes que utilizan HLS/CMAF, en el que a VECES EXT-X-MAP faltaba tokens de CDN o etiquetas EXT-X-MAP, a veces incorrectamente desplegadas fuera de la ventana de DVR.

### Versión 20.8.4

**Cuándo:** Miércoles, 19 de agosto de 2020 de 03:30 a.m. a 07:30 a.m. hora del este

**Mejoras y correcciones**

Actualizaciones de mantenimiento.

### Versión 20.8.1

**Cuándo:** Martes, 4 de agosto de 2020 de 3:00 a.m. a 6:00 a.m. hora del este

**Mejoras y correcciones**

Actualizaciones de mantenimiento.

### Versión 20.7.1

**Cuándo:** Jueves, 9 de julio de 2020 de 03:00 a.m. a 05:00 a.m., hora del este

**Nuevas funciones y mejoras**

* Mejora de SCTE35 para utilizar cualquiera de los mensajes de inicio/fin de anuncio de proveedor o los mensajes de inicio/fin de interrupción para identificar la señal.

* Se ha actualizado el encabezado X-ADBE-AI-X1 con información adicional para ayudar a solucionar problemas.

* Agregación de métricas mejorada.

* Tablero de la consola de SAI mejorado para el panel Estado de la sesión

### Versión 20.6.2

**Cuándo:** Jueves, 18 de junio de 2020 de 03:00 a.m. a 04:00 a.m., hora del este

**Mejoras**

Se ha mejorado la sincronización de flujos para clientes de vídeo que requieren precisión de milisegundos. Póngase en contacto con la asistencia técnica de Adobe para habilitar la precisión de milisegundos para `#EXT-X-PROGRAM-DATE-TIME tags`.

### Versión 20.6.1

**Cuándo:** Martes, 2 de junio de 2020 de 03:00 a.m. a 05:00 a.m., hora del este

**Nuevas funciones**

Póngase en contacto con la asistencia técnica del Adobe para habilitar las siguientes nuevas funciones mediante la configuración del lado del servidor:

* Manipulación de manifiestos: ahora, las direcciones URL de recursos y segmentos de HLS se pueden transformar entre HTTP y HTTPS para aumentar el rendimiento al reducir los protocolos de enlace TLS en solicitudes del back-end. También se puede utilizar para unificar fragmentos de contenido/publicidad en las mismas CDN.

* VOD de formulario largo: se han mejorado las API para mantener la conexión de la sesión con recursos de VOD de formulario largo.

**Correcciones de errores**

* Se ha corregido un problema en el cual los fragmentos WebVTT siempre se solicitaban bajo el protocolo http, independientemente del protocolo original solicitado.

* Se ha corregido un problema por el cual las etiquetas EXT-X-DISCONTINUITY se eliminaban de la parte superior de la lista de reproducción al cambiar de anuncios de vuelta al contenido. Póngase en contacto con Asistencia técnica de Adobe para habilitar esta corrección.

### Versión 20.5.1

**Cuándo:** Martes, 5 de mayo de 2020 de 04:00 a.m. a 05:00 a.m., hora del este

* Se ha corregido un problema para garantizar que se proporcionen encabezados CORS correctos cuando se envían encabezados If-Modified-Since.

* Correcciones de errores en el panel de CRS.

* Actualizaciones de mantenimiento.

### Versión 20.3.4

**Cuándo:** Miércoles, 1 de abril de 2020 de 03:00 a.m. a 04:00 a.m. hora del este

* Se ha corregido un problema que provocaba que los subtítulos no se sincronizaran después de la inserción de la publicidad en VOD/ WebVTT.

* Actualizaciones de seguridad.

### Versión 20.3.3

**Cuándo:** Jueves, 26 de marzo de 2020 de 03:00 a.m. a 04:00 a.m., hora del este

* Las respuestas SSAI 4XX y 5XX ahora proporcionan correctamente los encabezados relacionados con CORS, lo que permite a los clientes de vista web de JavaScript de dominios cruzados leer correctamente las respuestas de error.

* Se ha corregido un problema con los encabezados X-Forwarded-For, en el cual las direcciones IPv6 no se codificaban correctamente en la dirección URL al pasarlas a los servidores de publicidad.

* Se ha corregido un problema con los flujos de audio CMAF/demuxed, en el que en algunos casos los números EXT-X-MEDIA-SEQUENCE aumentaban incorrectamente.

### Versión 20.3.2

**Cuándo:** Miércoles, 11 de marzo de 2020 de 05:30 a.m. a 07:00 a.m. hora del este

* Mejoras en la gestión de señales SCTE35.

* Actualizaciones de mantenimiento.

### Versión 20.3.1

**Cuándo:** Jueves, 5 de marzo de 2020 de 02:30 a.m. a 04:30 a.m., hora del este

* Mejoras de rendimiento:

   * Se ha agregado compatibilidad con caché para ambos manifiestos m3u8 maestro/multimedia. Estos manifiestos ahora responden a los encabezados Cache-Control: public y Max-Age, que a menudo pueden mejorar el rendimiento del inicio del vídeo.

   * Se ha agregado compatibilidad para obligar a los creativos https a recuperarse a través de http, lo que también puede mejorar el rendimiento de inicio de vídeo.

* Correcciones de seguridad y mantenimiento.

### Versión 20.2.1

**Cuándo:** Jueves, 13 de febrero de 2020 de 04:30 a.m. a 05:30 a.m., hora del este

* Se ha agregado compatibilidad con la vinculación de recursos de publicidad que contienen varios flujos de solo audio basados en idioma/códec/velocidad de bits.
* Pequeñas mejoras de rendimiento y actualizaciones de mantenimiento.

### Versión 20.1.3

**Cuándo:** Martes, 28 de enero de 2020 de 2:00 a.m. a 03:00 a.m., hora del este

* **Compatibilidad con VMAP con FER para nbc CueFormat**

   Convertir las señales de flujo FER en parámetros de anulación de línea de tiempo FW, cuando `ptcueformat=nbc` y el flujo es un flujo de VOD con señales en manifiesto y anuncios predefinidos.

* Limpie el campo user-agent en el encabezado HTTP antes de reenviarlo a proveedores de publicidad de terceros/CDN.

* Filtre los caracteres de control/no imprimibles (código ASCII &lt; 32) de los encabezados HTTP user-agent antes de enviarlos a Auditude y otros proveedores de publicidad, CDN. Auditude Ad-Call solía fallar para estos encabezados no válidos.

* Purgue los objetos V1 antiguos de los grupos de NetStorage para mantener el recuento de objetos dentro de los límites seguros de Akamai.

### Versión 20.1.2 (revisión)

**Cuándo:** Lunes, 20 de enero de 2020 de 02:00 a.m. a 03:00 a.m. hora del este

* Actualizaciones de mantenimiento.

### Versión 20.1.1

**Cuándo:** Miércoles, 15 de enero de 2020 de 04:00 a.m. a 05:00 a.m. hora del este

* El Servicio de Reempaquetado Creativo ahora ofrece una inserción de anuncios más rápida mediante el bloqueo automático de la lista de creativos mal formados.

* Se ha añadido compatibilidad con la fase 1 del nuevo formato de señal SCTE 35 en la inserción de anuncios en el lado del servidor.

* Actualizaciones de mantenimiento.

## Problemas resueltos {#Resolved-issues}

Cuando la resolución está asociada con un problema informado, se muestra una referencia de Zendesk. Por ejemplo, `ZD#xxxxx`.

**PTAI 20.9.1**

* Se ha corregido el problema para los clientes que utilizan HLS/CMAF, en el que a VECES EXT-X-MAP faltaba tokens de CDN o etiquetas EXT-X-MAP, a veces incorrectamente desplegadas fuera de la ventana de DVR.

**PTAI 20.6.1**

* `WebVTT` los fragmentos siempre se solicitaban en el protocolo http, independientemente del protocolo original solicitado.

* `EXT-X-DISCONTINUITY` las etiquetas se eliminan de la parte superior de la lista de reproducción al cambiar de anuncios a contenido. Póngase en contacto con Asistencia técnica de Adobe para habilitar esta corrección.

**PTAI 20.5.1**

* Problemas con los encabezados CORS cuando se envían encabezados If-Modified-Since.

* Problemas en el panel de CRS.

**PTAI 20.3.4**

* Problema que provocaba que los subtítulos no se sincronizaran después de la inserción del anuncio en VOD/ WebVTT.

**PTAI 20.3.3**

* Problema con los encabezados X-Forwarded-For, donde las direcciones IPv6 no se codificaban correctamente en la dirección URL cuando se pasaban a los servidores de publicidad.

* Problema con los flujos de audio CMAF/demuxed, donde en ciertos casos los números EXT-X-MEDIA-SEQUENCE aumentan incorrectamente en ciertos casos

## Problemas y limitaciones conocidos

**PTAI 20.10.1**

No se ha añadido ninguna nueva limitación.
