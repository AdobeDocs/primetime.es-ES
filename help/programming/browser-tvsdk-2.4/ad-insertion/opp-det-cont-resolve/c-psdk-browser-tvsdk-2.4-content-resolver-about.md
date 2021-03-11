---
description: El TVSDK del explorador proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la cronología, y estos generadores y solucionadores se basan en etiquetas no estándar del manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades que se identifican en el manifiesto.
title: Generadores de oportunidades y solucionadores de contenido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Generadores de oportunidades y solucionadores de contenido{#opportunity-generators-and-content-resolvers}

El TVSDK del explorador proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la cronología, y estos generadores y solucionadores se basan en etiquetas no estándar del manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades que se identifican en el manifiesto.

Un *`opportunity`* representa un punto de interés en la cronología que normalmente indica una oportunidad de colocación de publicidad. Esta oportunidad también puede indicar una operación personalizada que podría afectar a la cronología. Un *`opportunity generator`* identifica oportunidades específicas (etiquetas) en la cronología y notifica a TVSDK que estas oportunidades se han etiquetado.

Las oportunidades se identifican en una cronología en `TimedMetata`. El `ManifestCuesOpportunityGenerator` crea oportunidades en función de los objetos `TimedMetadata` que se crean para cada etiqueta de publicidad de salida de empalme (en `MediaPlayerItemConfig.adTags`) que se ha detectado en el manifiesto. El `AdSignalingModeOpportunityGenerator` crea la oportunidad inicial basada en el tipo `MediaPlayerItem` y su modo de señalización de anuncio asociado.

>[!TIP]
>
>Si la propiedad `AdvertisingMetadata.livePreroll` o `AdvertisingMetadata.preroll` está establecida, `AdSignalingModeOpportunityGenerator` genera una oportunidad pre-roll para los flujos en vivo.

Cuando se notifica a la aplicación sobre una oportunidad (etiqueta), la aplicación podría modificar la cronología; por ejemplo, insertando una serie de anuncios. De forma predeterminada, el SDK de TVSDK del explorador llama al *`content resolver`* apropiado para implementar las acciones o cambios necesarios en la cronología. Su aplicación puede utilizar la resolución de contenido de publicidad TVSDK de navegador predeterminada o registrar su propia resolución de contenido.

También puede utilizar `MediaPlayerItemConfig.adTags` para agregar más etiquetas/indicaciones de marcadores de publicidad para la clase predeterminada `ManifestCuesOpportunityGenerator` y utilizar `MediaPlayerItemConfig.subscribedTags` para que TVSDK pueda notificar a la aplicación sobre etiquetas adicionales que puedan tener información de flujo de trabajo de publicidad.

>[!TIP]
>
>Los valores predeterminados de `MediaPlayerItemConfig.adTags` y `MediaPlayerItemConfig.subscribeTags` es `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.

