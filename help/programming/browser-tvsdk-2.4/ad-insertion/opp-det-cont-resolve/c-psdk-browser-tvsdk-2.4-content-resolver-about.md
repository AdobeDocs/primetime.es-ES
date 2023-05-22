---
description: Browser TVSDK proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la cronología. Estos generadores y solucionadores se basan en etiquetas no estándar en el manifiesto. Es posible que la aplicación tenga que modificar la cronología en función de las oportunidades identificadas en el manifiesto.
title: Generadores de oportunidades y solucionadores de contenido
exl-id: a47acd22-8b1b-4c66-a7eb-a4d99afb5f17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Generadores de oportunidades y solucionadores de contenido{#opportunity-generators-and-content-resolvers}

Browser TVSDK proporciona generadores de oportunidades predeterminados y solucionadores de contenido que colocan anuncios en la cronología. Estos generadores y solucionadores se basan en etiquetas no estándar en el manifiesto. Es posible que la aplicación tenga que modificar la cronología en función de las oportunidades identificadas en el manifiesto.

Un *`opportunity`* representa un punto de interés en la cronología que generalmente indica una oportunidad de ubicación de publicidad. Esta oportunidad también puede indicar una operación personalizada que podría afectar a la cronología. Un *`opportunity generator`* identifica oportunidades específicas (etiquetas) en la cronología y notifica a TVSDK que estas oportunidades se han etiquetado.

Las oportunidades se identifican en una cronología en `TimedMetata`. El `ManifestCuesOpportunityGenerator` crea oportunidades basadas en el `TimedMetadata` objetos creados para cada etiqueta de anuncio de empalme (en `MediaPlayerItemConfig.adTags`) que se ha detectado en el manifiesto. El `AdSignalingModeOpportunityGenerator` crea la oportunidad inicial basada en la variable `MediaPlayerItem` tipo y su modo de señalización de anuncio asociado.

>[!TIP]
>
>Si la variable `AdvertisingMetadata.livePreroll` o el `AdvertisingMetadata.preroll` se ha establecido la propiedad, `AdSignalingModeOpportunityGenerator` genera una oportunidad previa a la emisión para las emisiones en directo.

Cuando se notifica a la aplicación sobre una oportunidad (etiqueta), esta puede modificar la cronología, por ejemplo, insertando una serie de anuncios. De forma predeterminada, el TVSDK del explorador llama al método apropiado *`content resolver`* para implementar los cambios o las acciones de cronología necesarios. Su aplicación puede utilizar el solucionador de contenido de anuncio de TVSDK del explorador predeterminado o registrar su propio solucionador de contenido.

También puede utilizar `MediaPlayerItemConfig.adTags` para añadir más etiquetas/señales de marcador de anuncio para el valor predeterminado `ManifestCuesOpportunityGenerator` clase y uso `MediaPlayerItemConfig.subscribedTags` para que TVSDK pueda notificar a su aplicación sobre etiquetas adicionales que puedan tener información de flujo de trabajo de publicidad.

>[!TIP]
>
>Los valores predeterminados de `MediaPlayerItemConfig.adTags` y `MediaPlayerItemConfig.subscribeTags` es `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.
