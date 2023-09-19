---
title: Almacenamiento en caché
description: Almacenamiento en caché
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Almacenamiento en caché HTTP {#caching}

De forma predeterminada, el Ad Insertion de Primetime respeta los encabezados de control de caché HTTP al recuperar contenido y elementos creativos.  Esto puede reducir drásticamente la cantidad de solicitudes de red necesarias para que el Ad Insertion de Primetime realice a la CDN en todos los clientes.  Para el almacenamiento en caché, Adobe recomienda las siguientes configuraciones e implica el envío del encabezado HTTP `max-age` desde su CDN.  Póngase en contacto con su representante de CDN para habilitar estos encabezados en las transmisiones de vídeo y las transmisiones de anuncios.

## Para contenido en directo/lineal {#caching-live-linear-content}

* Manifiesto maestro: 24 horas o Cache-Control: max-age=86400
* Manifiesto de medios: 1 segundo o Cache-Control: max-age=1

## Para contenido de VOD {#caching-vod-content}

* Manifiesto maestro: 24 horas o Cache-Control: max-age=86400
* Manifiesto de medios: 24 horas o Cache-Control: max-age=86400
