---
title: Usar Ad Insertion para VOD
description: Uso de Ad Insertion para VOD
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Usar Ad Insertion para VOD {#ad-insertion-vod}

El Ad Insertion Primetime admite la inserción de anuncios en varios recursos de VOD, con los formatos estándar VAST 3.0+ o VMAP 1.0+.

* [VMAP de IAB](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD (anuncios con asignación de servidor) {#server-mapped-ads}

El Ad Insertion Primetime admite la inserción de VOD con anuncios insertados antes del comienzo de la reproducción mediante la información de líneas de tiempo de anuncios definida en un formato VMAP.  El seguimiento de anuncios específicos de VMAP, como las señalizaciones breakStart/breakEnd, se entregará con [Seguimiento de anuncios](set-up-ad-tracking.md).

## Reproducción de Evento completo (VOD con señales de Ad Decisioning) {#full-event-replay}

Primetime Ad Insertion también admite recursos VOD especializados que contienen señales en el flujo de contenido, como las que se encuentran en la reproducción de eventos en directo grabados anteriormente. Para obtener más información sobre los tipos de señales de decisión de publicidad (o formatos de señal) que admitimos, consulte [Uso de Ad Insertion en Live/Linear](ad-insertion-live-linear-stream.md).

Se admiten escenarios de solicitud de publicidad única y de solicitud de publicidad múltiple en paralelo para los recursos de VOD que contienen más de una pausa publicitaria. Para obtener más información, consulte el parámetro `ptmulticall` en [Descripción del parámetro](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md). Los formatos VAST y VMAP son compatibles con las señales en flujo.
