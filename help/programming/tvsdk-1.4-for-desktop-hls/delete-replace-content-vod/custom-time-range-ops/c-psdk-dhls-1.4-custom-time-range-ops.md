---
description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.
seo-description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.
seo-title: Operaciones de intervalo de tiempo personalizado
title: Operaciones de intervalo de tiempo personalizado
uuid: fb27f343-718d-444e-8fc1-5ae0be02557b
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Información general {#custom-time-range-operations-overview}

TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.

La función Eliminar y reemplazar amplía la función de marcadores de publicidad personalizados. Los marcadores de publicidad personalizados marcan secciones del contenido principal como períodos de contenido relacionados con la publicidad. Además de marcar estos intervalos de tiempo, también puede eliminar y reemplazar dichos intervalos.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

La eliminación y sustitución de publicidades se implementan con marcadores personalizados que identifican distintos tipos de intervalos de tiempo en un flujo VOD: marcar, eliminar y reemplazar. Para cada intervalo de tiempo personalizado, puede realizar operaciones asociadas, incluida la eliminación o sustitución del contenido de la publicidad.

Para la eliminación y sustitución de publicidades, TVSDK incluye los siguientes modos de operación *de intervalo de tiempo* personalizados:

* MARK: distribuye `AdBreak` eventos para las regiones marcadas. (Esto se llamaba `customAdMarker` en versiones anteriores de TVSDK). No se permite la inserción de anuncios en este modo.

* ELIMINAR: para este modo, la aplicación utiliza la `TimeRangeCollection` clase para definir las regiones horarias para la eliminación de anuncios en C3. Se permite la inserción de anuncios en este modo.
* REEMPLAZAR: En este modo, la aplicación reemplaza un anuncio `timeRange` por una toma de decisiones de anuncios de Adobe Primetime `AdBreak`. La operación de reemplazo comienza donde se produce la eliminación de la publicidad C3 y termina en el tiempo indicado (más corto o más que el intervalo de tiempo original).

TVSDK proporciona una `CustomRangesOpportunityGenerator` clase para generar oportunidades de colocación para los rangos MARK y DELETE. Para el modo REPLACE, TVSDK genera dos oportunidades de colocación para cada intervalo de tiempo:

* Genera `CustomRangeResolver` oportunidades de colocación para ELIMINAR
* El `AuditudeAdResolver` genera oportunidades de colocación para INSERT.