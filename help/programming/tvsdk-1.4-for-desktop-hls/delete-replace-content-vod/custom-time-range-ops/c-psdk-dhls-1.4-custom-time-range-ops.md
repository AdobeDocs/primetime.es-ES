---
description: TVSDK admite la eliminación y el reemplazo mediante programación del contenido de anuncios en flujos de VOD.
title: Operaciones de intervalo de tiempo personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Información general {#custom-time-range-operations-overview}

TVSDK admite la eliminación y el reemplazo mediante programación del contenido de anuncios en flujos de VOD.

La función Eliminar y reemplazar amplía la función de marcadores de publicidad personalizados. Los marcadores de publicidad personalizados marcan secciones del contenido principal como periodos de contenido relacionados con anuncios. Además de marcar estos intervalos de tiempo, también puede eliminar y reemplazar intervalos de tiempo.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

La eliminación y el reemplazo de anuncios se implementan con marcadores personalizados que identifican diferentes tipos de intervalos de tiempo en un flujo de VOD: marcar, eliminar y reemplazar. Para cada intervalo de tiempo personalizado, puede realizar operaciones asociadas, incluida la eliminación o sustitución de contenido de un anuncio.

Para eliminar y reemplazar anuncios, TVSDK incluye lo siguiente *operación de intervalo de tiempo personalizado* modos:

* MARCAR: envíos `AdBreak` eventos para las regiones marcadas. (Se ha llamado `customAdMarker` en versiones anteriores de TVSDK). No se permite la inserción de anuncios en este modo.

* DELETE: para este modo, la aplicación utiliza el `TimeRangeCollection` para definir las regiones horarias de eliminación de anuncios de C3. En este modo se permite la inserción de anuncios.
* REEMPLAZAR: en este modo, la aplicación reemplaza a `timeRange` con una Adobe Primetime ad decisioning `AdBreak`. La operación de reemplazo comienza donde se produce la eliminación del anuncio C3 y finaliza en el momento indicado (más corto o más largo que el intervalo de tiempo original).

TVSDK proporciona un `CustomRangesOpportunityGenerator` para generar oportunidades de colocación para los rangos MARK y DELETE. Para el modo REEMPLAZAR, TVSDK genera dos oportunidades de colocación para cada intervalo de tiempo:

* El `CustomRangeResolver` genera oportunidades de colocación para el DELETE
* El `AuditudeAdResolver` genera oportunidades de colocación para INSERT.
