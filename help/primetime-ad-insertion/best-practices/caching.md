---
title: Almacenamiento en caché
description: null
translation-type: tm+mt
source-git-commit: 76dc54fabdae400ad708ba83fcf6f7fd5caa2b22
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Almacenamiento en caché HTTP {#caching}

De forma predeterminada, Primetime Ad Insertion respeta los encabezados de control de caché HTTP al recuperar elementos creativos publicitarios así como contenido.  Esto puede reducir drásticamente la cantidad de solicitudes de red necesarias para que Primetime Ad Insertion las realice en la CDN en todos los clientes.  Para el almacenamiento en caché, Adobe recomienda la siguiente configuración y supone enviar el encabezado HTTP `max-age` desde su CDN.  Póngase en contacto con el representante de CDN para habilitar estos encabezados en los flujos de vídeo y los flujos de anuncios.

## Para contenido en directo/lineal {#caching-live-linear-content}

* Manifiesto maestro: 24 horas, o Cache-Control: max-age=86400
* Manifiesto de medios: 1 segundo o Cache-Control: max-age=1

## Para contenido de VOD {#caching-vod-content}

* Manifiesto maestro: 24 horas, o Cache-Control: max-age=86400
* Manifiesto de medios: 24 horas, o Cache-Control: max-age=86400
