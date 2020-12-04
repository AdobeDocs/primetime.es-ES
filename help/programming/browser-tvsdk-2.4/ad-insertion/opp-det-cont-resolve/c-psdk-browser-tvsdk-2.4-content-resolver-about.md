---
description: El SDK TVSDK del explorador proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan publicidades en la línea de tiempo, y estos generadores y solucionadores se basan en etiquetas no estándar del manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades identificadas en el manifiesto.
seo-description: El SDK TVSDK del explorador proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan publicidades en la línea de tiempo, y estos generadores y solucionadores se basan en etiquetas no estándar del manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades identificadas en el manifiesto.
seo-title: Generadores de oportunidades y solucionadores de contenido
title: Generadores de oportunidades y solucionadores de contenido
uuid: e462ad89-1609-4efa-aa67-cfd04f045927
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Generadores de oportunidades y solucionadores de contenido{#opportunity-generators-and-content-resolvers}

El SDK TVSDK del explorador proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan publicidades en la línea de tiempo, y estos generadores y solucionadores se basan en etiquetas no estándar del manifiesto. Es posible que la aplicación necesite modificar la cronología en función de las oportunidades identificadas en el manifiesto.

Un *`opportunity`* representa un punto de interés en la cronología que generalmente indica una oportunidad de colocación de publicidad. Esta oportunidad también puede indicar una operación personalizada que podría afectar a la línea de tiempo. Un *`opportunity generator`* identifica oportunidades específicas (etiquetas) en la línea de tiempo y notifica al TVSDK que estas oportunidades se han etiquetado.

Las oportunidades se identifican en una cronología en `TimedMetata`. El `ManifestCuesOpportunityGenerator` crea oportunidades basadas en los objetos `TimedMetadata` que se crean para cada etiqueta de publicidad de salida de empalme (en `MediaPlayerItemConfig.adTags`) detectada en el manifiesto. El `AdSignalingModeOpportunityGenerator` crea la oportunidad inicial basada en el tipo `MediaPlayerItem` y su modo de señalización de publicidad asociado.

>[!TIP]
>
>Si se establece la propiedad `AdvertisingMetadata.livePreroll` o `AdvertisingMetadata.preroll`, `AdSignalingModeOpportunityGenerator` genera una oportunidad de predesplazamiento para flujos activos.

Cuando se notifica a la aplicación sobre una oportunidad (etiqueta), puede que la aplicación modifique la escala de tiempo; por ejemplo, insertando una serie de publicidades. De forma predeterminada, TVSDK del explorador llama a la *`content resolver`* adecuada para implementar los cambios o acciones de línea de tiempo necesarios. La aplicación puede utilizar la resolución de contenido de publicidad TVSDK del explorador predeterminada o registrar su propia resolución de contenido.

También puede utilizar `MediaPlayerItemConfig.adTags` para agregar más etiquetas/indicaciones de marcadores de publicidad para la clase predeterminada `ManifestCuesOpportunityGenerator` y utilizar `MediaPlayerItemConfig.subscribedTags` para que TVSDK pueda notificar a la aplicación sobre etiquetas adicionales que puedan tener información de flujo de trabajo de publicidad.

>[!TIP]
>
>Los valores predeterminados de `MediaPlayerItemConfig.adTags` y `MediaPlayerItemConfig.subscribeTags` es `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.

