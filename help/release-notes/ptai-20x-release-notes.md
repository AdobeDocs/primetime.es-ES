---
title: Notas de la versión de PTAI 20.5.1
description: Las notas de la versión de PTAI 20.5.1 describen las novedades o los cambios que se han producido en la inserción de publicidad dinámica de Primetime en el año 2020.
translation-type: tm+mt
source-git-commit: 266b884707e9160d539a06fd089732ef8ade21ba
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# Notas de la versión 20.5.1 de Primetime Dynamic Ad Insertion

Las notas de la versión de Inserción de publicidad dinámica 20.5.1 describen las novedades o los cambios, los problemas resueltos y los problemas conocidos en la inserción de publicidad dinámica de Primetime en el año 2020.

## Novedades de PTAI 20.5.1

**Cuando:** Martes 5 de mayo de 2020, de las 4:00 a las 5:00 AM ESTE

* Se ha corregido un problema para garantizar que se proporcionen encabezados CORS correctos al enviar encabezados If-Modified-Since.

* Corrección de errores en el panel CRS.

* Actualizaciones de mantenimiento.

## Qué ha cambiado en versiones anteriores

### Versión 20.3.4

**Cuando:** Miércoles 1 de abril de 2020, de 03:00 a 04:00 AM ESTE

* Se ha corregido un problema que provocaba que los subtítulos no estuvieran sincronizados tras la inserción de anuncios en VOD/ WebVTT.

* Actualizaciones de seguridad.

### Versión 20.3.3

**Cuando:** Jueves 26 de marzo de 2020 de 3:00 a 04:00 am ESTE

* Las respuestas de SSAI 4XX y 5XX ahora proporcionan correctamente encabezados relacionados con CORS, lo que permite a los clientes de javascript/webview entre dominios leer correctamente las respuestas de error.

* Se corrigió un problema con los encabezados X-Forwarded-For, donde las direcciones IPv6 no se codificaban correctamente en la dirección URL cuando se pasaban a los servidores de publicidad.

* Se corrigió un problema con los flujos de audio CMAF/desmuestreados, en el cual en determinados escenarios los números EXT-X-MEDIA-SEQUENCE se incrementaban incorrectamente.

### Versión 20.1.3

**Cuando:** Martes, 28 de enero de 2020 de las 2:00 a las 03:00 am ESTE

* **VMAP con compatibilidad FER para nbc CueFormat**

   Convertir señales del flujo FER en parámetros de anulación de línea de tiempo FW, cuando `ptcueformat=nbc` se utiliza y el flujo es un flujo VOD con señales en manifiesto y anuncios integrados.

* Sanice el campo user-agent en el encabezado HTTP antes de reenviarlo a proveedores de publicidad de terceros/CDN.

* Filtre los caracteres de control/no imprimibles (código ASCII &lt; 32) de los encabezados HTTP de usuario-agente antes de enviarlos a Auditude y otros proveedores de publicidad, CDN. Auditude Ad-Call solía fallar para encabezados no válidos.

* Purgue los objetos V1 antiguos de los grupos de NetStorage para mantener el recuento de objetos dentro de los límites seguros de Akamai.

## Problemas resueltos

Cuando la resolución está asociada a un problema informado, se muestra una referencia de Zendesk. Por ejemplo, ZD#xxxxx.

**PTAI 20.3.3**

* Problema con los encabezados X-Forwarded-For, donde las direcciones IPv6 no se codificaban correctamente en la dirección URL cuando se pasaban a los servidores de publicidad.

* Problema con los flujos de audio CMAF/desmuestreados, donde en determinados escenarios los números EXT-X-MEDIA-SEQUENCE aumentan incorrectamente en determinados escenarios

## Problemas y limitaciones conocidos

**PTAI 20.3.3**

No se ha agregado ninguna nueva limitación.
