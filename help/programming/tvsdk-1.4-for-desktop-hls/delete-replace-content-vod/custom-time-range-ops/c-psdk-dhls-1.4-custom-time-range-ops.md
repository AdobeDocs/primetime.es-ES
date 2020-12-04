---
description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.
seo-description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.
seo-title: Operaciones de intervalo de tiempo personalizado
title: Operaciones de intervalo de tiempo personalizado
uuid: fb27f343-718d-444e-8fc1-5ae0be02557b
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# Información general {#custom-time-range-operations-overview}

TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.

La función Eliminar y reemplazar amplía la función de marcadores de publicidad personalizados. Los marcadores de publicidad personalizados marcan secciones del contenido principal como períodos de contenido relacionados con la publicidad. Además de marcar estos intervalos de tiempo, también puede eliminar y reemplazar dichos intervalos.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

La eliminación y sustitución de publicidades se implementan con marcadores personalizados que identifican distintos tipos de intervalos de tiempo en un flujo VOD: marcar, eliminar y reemplazar. Para cada intervalo de tiempo personalizado, puede realizar operaciones asociadas, incluida la eliminación o sustitución del contenido de la publicidad.

Para la eliminación y sustitución de publicidades, TVSDK incluye los siguientes modos *de operación de intervalo de tiempo personalizado*:

* MARK: distribuye `AdBreak` eventos para las regiones marcadas. (Esto se llamaba `customAdMarker` en versiones anteriores de TVSDK). No se permite la inserción de anuncios en este modo.

* DELETE: para este modo, la aplicación utiliza la clase `TimeRangeCollection` para definir las regiones horarias para la eliminación de publicidad en C3. Se permite la inserción de anuncios en este modo.
* REEMPLAZAR: En este modo, la aplicación reemplaza un `timeRange` por una decisión de publicidad para Adobe Primetime `AdBreak`. La operación de reemplazo inicio dónde se produce la eliminación de publicidad C3 y termina en el tiempo indicado (más corto o más que el intervalo de tiempo original).

TVSDK proporciona una clase `CustomRangesOpportunityGenerator` para generar oportunidades de colocación para los rangos MARK y DELETE. Para el modo REPLACE, TVSDK genera dos oportunidades de colocación para cada intervalo de tiempo:

* El `CustomRangeResolver` genera oportunidades de colocación para el DELETE
* El `AuditudeAdResolver` genera oportunidades de colocación para INSERT.