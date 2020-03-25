---
title: Notas de la versión de PTAI 20.3.3
description: Las notas de la versión de PTAI 20.3.3 describen las novedades o los cambios que se han producido en la inserción de publicidad dinámica de Primetime en el año 2020.
translation-type: tm+mt
source-git-commit: ededb36a0b460fff4644a3716b36971ff9454c37

---


# Notas de la versión 20.3.3 de Primetime Dynamic Ad Insertion

Las notas de la versión de Inserción dinámica de publicidad 20.3.3 describen las novedades o los cambios, los problemas resueltos y los problemas conocidos en Inserción dinámica de publicidad en Primetime en el año 2020.

## Novedades de PTAI 20.3.3

**Cuando:** Jueves 26 de marzo de 2020 de 3:00 a 04:00 am ESTE

* Las respuestas de SSAI 4XX y 5XX ahora proporcionan correctamente encabezados relacionados con CORS, lo que permite a los clientes de javascript/webview entre dominios leer correctamente las respuestas de error.

* Se corrigió un problema con los encabezados X-Forwarded-For, donde las direcciones IPv6 no se codificaban correctamente en la dirección URL cuando se pasaban a los servidores de publicidad.

* Se corrigió un problema con los flujos de audio CMAF/desmuestreados, en el cual en determinados escenarios los números EXT-X-MEDIA-SECUENCE se incrementaban incorrectamente

## Qué ha cambiado en versiones anteriores

### Versión

**Cuando:**

### Versión

**Cuando:**

## Problemas resueltos

Cuando la resolución está asociada a un problema informado, se muestra una referencia de Zendesk. Por ejemplo, ZD#xxxxx.

**PTAI 20.3.3**

* Problema con los encabezados X-Forwarded-For, donde las direcciones IPv6 no se codificaban correctamente en la dirección URL cuando se pasaban a los servidores de publicidad.

* Problema con los flujos de audio CMAF/desmuestreados, donde en determinados escenarios los números EXT-X-MEDIA-SEQUENCE aumentan incorrectamente en determinados escenarios

## Problemas y limitaciones conocidos

**PTAI 20.3.3**

No se ha agregado ninguna nueva limitación.
