---
title: Integrar su CDN
description: Integración de la CDN
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Integrar su CDN {#integrating-cdn}

Primetime Ad Insertion sirve como proxy entre la aplicación cliente y los manifiestos, no los propios fragmentos de vídeo. Implemente el contenido en la CDN elegida y pase la dirección URL al Ad Insertion Primetime mediante la API de Bootstrap.<!-- For integration details, see [Supported CDNs](supported-cdns.md).-->

## Esquemas de tokenización CDN admitidos {#cdn-tokenization-schemes}

Las CDN suelen tener distintos esquemas de tokenización para la autorización de fragmentos. Primetime Ad Insertion admite de forma nativa las principales redes CDN, incluidas:

* Akamai
* Limelight
* Centurylink / Level3
* Póngase en contacto con su representante de asistencia técnica de Primetime para obtener una lista completa de las CDN admitidas

Para obtener más información sobre el parámetro `pttoken`, consulte [Descripción del parámetro API de Bootstrap](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md).

## Configure las publicidades que se van a enviar desde la CDN de contenido {#configure-ad-deliver-from-cdn}

Es posible que desee enviar publicidades y contenido desde la misma CDN para mantener la afinidad de contenido, ayudar a evitar los bloqueadores de publicidad y/o optimizar el número de conexiones requeridas desde la aplicación cliente. Primetime Ad Insertion admite reglas de reescritura de fragmentos para asignar fragmentos a la CDN de contenido.

<!--## Increase start-up performance with your CDN {#increase-startup-performance}

For more information, see [Optimizing start-up](optimize-video-startup-time.md).-->

## Funciones de Multi-CDN {#enable-multi-cdn-fetures}

Póngase en contacto con el representante de asistencia técnica de Primetime para habilitar las funciones de varios CDN.
