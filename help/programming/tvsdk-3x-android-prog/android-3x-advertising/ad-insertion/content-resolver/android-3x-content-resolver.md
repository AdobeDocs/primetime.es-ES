---
description: Un generador de oportunidades identifica las oportunidades de ubicación mediante etiquetas personalizadas en un flujo, modo de señalización, marcadores personalizados, etc. El generador de oportunidades envía estas oportunidades de colocación al solucionador de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.
title: Personalizar generadores de oportunidades y solucionadores de contenido
exl-id: 5d0ebaa6-4708-4602-b9d7-882c389fb030
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Información general {#customize-opportunity-generators-and-content-resolvers-overview}

Un generador de oportunidades identifica las oportunidades de ubicación mediante etiquetas personalizadas en un flujo, modo de señalización, marcadores personalizados, etc. El generador de oportunidades envía estas oportunidades de colocación al solucionador de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.

TVSDK incluye los siguientes generadores de oportunidades predeterminados:

* `ManifestCuesOpportunityGenerator` genera oportunidades a partir de las señales de publicidad predeterminadas ( `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` genera una oportunidad inicial para el modo de señalización de anuncio especificado. Esto ignora cualquier señal o información de metadatos cronometrada.
* `CustomMarkerOpportunityGenerator` genera oportunidades para reemplazar anuncios C3 precocinados.
* `AuditudeResolver`El generador de oportunidades de produce oportunidades cuando la resolución de anuncios diferidos está activada.

TVSDK también incluye solucionadores de contenido predeterminados:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, que puede comunicarse con Primetime y Decisioning.

Puede anular los generadores de oportunidades y los solucionadores de contenido predeterminados para personalizar el flujo de trabajo de publicidad de las siguientes maneras:

* Reconocer las etiquetas personalizadas para la inserción de anuncios. Para obtener más información, consulte [Personalizar generadores de oportunidades y solucionadores de contenido](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md).
* Cree un proveedor de publicidad personalizado.
* Contenido en negro.
