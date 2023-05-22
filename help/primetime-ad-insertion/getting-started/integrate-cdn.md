---
title: Integración de su CDN
description: Integración de su CDN
exl-id: b93031a2-6e66-4de1-9cf2-b0260f88fe13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Integración de su CDN {#integrating-cdn}

El Ad Insertion de Primetime sirve como proxy entre la aplicación cliente y los manifiestos, no los propios fragmentos de vídeo. Implemente el contenido en la red de distribución de contenido (CDN) que desee y pase la URL al Ad Insertion de Primetime mediante la API de Bootstrap. Para obtener más información sobre la integración, consulte [CDN compatibles](/help/primetime-ad-insertion/technical-reference/supported-cdns.md).

## Esquemas de tokenización de CDN admitidos {#cdn-tokenization-schemes}

Las CDN suelen tener diferentes esquemas de tokenización para la autorización de fragmentos. El Ad Insertion de Primetime admite de forma nativa las principales redes CDN, incluidas:

* Akamai
* Limelight
* Centurylink / Level3
* Póngase en contacto con su representante de asistencia técnica de Primetime para obtener una lista completa de las CDN admitidas

Para obtener más información sobre `pttoken` parámetro, consulte [Descripción del parámetro de API del Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description).

## Configuración de anuncios para su envío desde la CDN de contenido {#configure-ad-deliver-from-cdn}

Es posible que desee enviar anuncios y contenido desde la misma CDN para mantener la afinidad del contenido, ayudar a evitar los bloqueadores de anuncios y/o optimizar el número de conexiones necesarias desde la aplicación cliente. El Ad Insertion de Primetime admite reglas de reescritura de fragmentos para asignar fragmentos a la CDN de contenido. Para obtener más información, consulte [Reescritura de manifiesto](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md).

## Aumente el rendimiento de inicio con su CDN {#increase-startup-performance}

Para obtener más información, consulte [Optimización del inicio](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md).

## Funciones de varias CDN {#enable-multi-cdn-fetures}

Póngase en contacto con el representante de asistencia técnica de Primetime para habilitar varias funciones de CDN.
