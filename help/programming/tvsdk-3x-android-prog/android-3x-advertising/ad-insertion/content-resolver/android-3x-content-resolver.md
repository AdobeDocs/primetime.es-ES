---
description: Un generador de oportunidades identifica las oportunidades de colocación mediante etiquetas personalizadas en un flujo, marcadores personalizados del modo de señalización de publicidad, etc. El generador de oportunidades envía estas oportunidades de colocación a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.
seo-description: Un generador de oportunidades identifica las oportunidades de colocación mediante etiquetas personalizadas en un flujo, marcadores personalizados del modo de señalización de publicidad, etc. El generador de oportunidades envía estas oportunidades de colocación a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.
seo-title: Personalización de los generadores de oportunidades y los solucionadores de contenido
title: Personalización de los generadores de oportunidades y los solucionadores de contenido
uuid: 0d4fb0b2-98f3-4245-9bf1-4e968c5d0f36
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Información general {#customize-opportunity-generators-and-content-resolvers-overview}

Un generador de oportunidades identifica las oportunidades de colocación mediante etiquetas personalizadas en un flujo, marcadores personalizados del modo de señalización de publicidad, etc. El generador de oportunidades envía estas oportunidades de colocación a la resolución de contenido, que personaliza el flujo de trabajo de inserción de contenido/publicidad en función de las propiedades y los metadatos de la oportunidad de colocación.

TVSDK incluye los siguientes generadores de oportunidades predeterminados:

* `ManifestCuesOpportunityGenerator` genera oportunidades a partir de las señales de publicidad predeterminadas ( `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` genera una oportunidad inicial para el modo de señalización de publicidad especificado. Esto ignora cualquier señal o información de metadatos temporizados.
* `CustomMarkerOpportunityGenerator` genera oportunidades para reemplazar las publicidades C3 incorporadas.
* `AuditudeResolver`El generador de oportunidades de Omniture genera oportunidades cuando la resolución perezosa de anuncios está activada.

TVSDK también incluye los resueltores de contenido predeterminados:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, que pueden comunicarse con Primetime y la toma de decisiones.

Puede anular los generadores de oportunidades y los solucionadores de contenido predeterminados para personalizar el flujo de trabajo de la publicidad de formas como las siguientes:

* Reconocer etiquetas personalizadas para la inserción de publicidades. Para obtener más información, consulte [Personalización de generadores de oportunidades y solucionadores](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md)de contenido.
* Cree un proveedor de publicidad personalizado.
* Desactivar contenido.