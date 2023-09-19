---
title: Usar Ad Insertion para VOD
description: Uso del Ad Insertion para VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Usar Ad Insertion para VOD {#ad-insertion-vod}

El Ad Insertion de Primetime admite la inserción de anuncios en varios recursos de VOD mediante formatos estándar VAST 3.0+ o VMAP 1.0+.

* [VMAP IAB](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD (mapas de anuncios) {#server-mapped-ads}

El Ad Insertion de Primetime admite la inserción de VOD con anuncios insertados antes del comienzo de la reproducción mediante información de cronología de anuncio definida en formato VMAP.  El seguimiento de anuncios específico de VMAP, como las señalizaciones breakStart/breakEnd, se entregará con [Seguimiento de publicidad](set-up-ad-tracking.md).

## Reproducción completa de eventos (VOD con señales de Ad Decisioning) {#full-event-replay}

Primetime Ad Insertion también admite recursos de VOD especializados que contienen indicaciones en el propio flujo de contenido, como los que se encuentran en la reproducción de eventos en directo grabados anteriormente. Para obtener más información sobre los tipos de señales de decisión de anuncios (o formatos de referencia) compatibles, consulte [Uso del Ad Insertion en directo/lineal](ad-insertion-live-linear-stream.md).

Admitimos escenarios de solicitud de anuncio único y de solicitud de anuncio múltiple paralelo para recursos de VOD que contienen más de una pausa publicitaria. Para obtener más información, consulte `ptmulticall` parámetro en [Descripción del parámetro](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md). Los formatos VAST y VMAP son compatibles con las señales en flujo.
