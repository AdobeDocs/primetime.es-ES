---
description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos de VOD.
title: Operaciones de intervalos de tiempo personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Información general {#custom-time-range-operations-overview}

TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos de VOD.

La función de eliminar y reemplazar amplía la función de marcadores de anuncios personalizados. Los marcadores de anuncios personalizados marcan secciones del contenido principal como períodos de contenido relacionado con la publicidad. Además de marcar estos intervalos de tiempo, también puede eliminar y reemplazar intervalos de tiempo.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

La eliminación y el reemplazo de anuncios se implementan con marcadores personalizados que identifican diferentes tipos de intervalos de tiempo en un flujo de VOD: marcar, eliminar y reemplazar. Para cada intervalo de tiempo personalizado, puede realizar operaciones asociadas, como eliminar o reemplazar contenido de publicidad.

Para la eliminación y sustitución de anuncios, TVSDK incluye los siguientes modos *de operación de intervalo de tiempo personalizado*:

* MARK: envía eventos `AdBreak` para las regiones marcadas. (Esto se llamaba `customAdMarker` en versiones anteriores de TVSDK). No se permite la inserción de publicidad en este modo.

* DELETE : para este modo, la aplicación utiliza la clase `TimeRangeCollection` para definir las regiones horarias de eliminación de anuncios C3. Se permite la inserción de publicidad en este modo.
* REEMPLAZAR: En este modo, la aplicación sustituye a `timeRange` por una `AdBreak` de Adobe Primetime ad decisioning. La operación de reemplazo comienza donde se produce la eliminación de publicidad C3 y termina en el momento indicado (más corto o más largo que el intervalo de tiempo original).

TVSDK proporciona una clase `CustomRangesOpportunityGenerator` para generar oportunidades de colocación para los rangos MARK y DELETE. Para el modo REPLACE , TVSDK genera dos oportunidades de colocación para cada intervalo de tiempo:

* El `CustomRangeResolver` genera oportunidades de ubicación para el DELETE
* El `AuditudeAdResolver` genera oportunidades de colocación para INSERT.