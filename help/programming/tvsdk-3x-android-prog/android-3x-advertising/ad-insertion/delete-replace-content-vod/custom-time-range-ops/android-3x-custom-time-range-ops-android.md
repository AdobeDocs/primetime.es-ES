---
description: La clase CustomRangeMetadata identifica distintos tipos de intervalos de tiempo en un flujo de VOD para marcar, eliminar y reemplazar. Para cada uno de estos tipos de intervalos de tiempo personalizados, puede realizar las operaciones correspondientes, incluida la eliminación y el reemplazo del contenido de la publicidad.
title: Operaciones de intervalo de tiempo personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Operaciones de intervalo de tiempo personalizadas {#custom-time-range-operations}

La clase CustomRangeMetadata identifica diferentes tipos de intervalos de tiempo en un flujo de VOD: marcar, eliminar y reemplazar. Para cada uno de estos tipos de intervalos de tiempo personalizados, puede realizar las operaciones correspondientes, incluida la eliminación y el reemplazo del contenido de la publicidad.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

Para eliminar y reemplazar anuncios, TVSDK utiliza lo siguiente *operación de intervalo de tiempo personalizado* modos:

* **MARCAR** Este modo se denominaba marcadores de anuncios personalizados en versiones anteriores de TVSDK. El modo marca las horas de inicio y finalización para los anuncios que ya se han colocado en el flujo de VOD. Cuando hay marcadores de intervalo de tiempo de tipo `MARK` en la secuencia, una ubicación inicial de `Mode.MARK` es generado por `CustomMarkerOpportunityGenerator` y resuelto por `CustomRangeResolver`. No se han insertado anuncios.

* **DELETE** Para `DELETE` intervalos de tiempo, una `placementInformation` de tipo `Mode.DELETE` lo crea y resuelve `CustomRangeResolver`. `DeleteRangeTimelineOperation` define los intervalos que se eliminarán de la cronología y TVSDK utiliza `removeByLocalTime` de la API de Adobe Video Engine (AVE) para completar esta operación. Si hay intervalos de DELETE y metadatos de Adobe Primetime y Decisioning, los intervalos se eliminan primero y, a continuación, la variable `AuditudeResolver` resuelve los anuncios mediante el flujo de trabajo típico de Adobe Primetime ad decisioning.

* **REPLACE** Para `REPLACE` intervalos de tiempo, dos iniciales `placementInformations` se crean, uno `Mode.DELETE` y uno `Mode.REPLACE`. `CustomRangeResolver` elimina primero los intervalos de tiempo y, a continuación, el `AuditudeResolver` inserta anuncios del especificado `replaceDuration` en la cronología. Si no `replaceDuration` se especifica, el servidor determina qué se inserta.

Para admitir estas operaciones de intervalo de tiempo personalizado, TVSDK proporciona lo siguiente:

* Varias resoluciones de contenido

  Un flujo puede tener varias resoluciones de contenido basadas en el modo de señalización de publicidad y los metadatos de publicidad. El comportamiento cambia con diferentes combinaciones de modos de señalización de publicidad y metadatos de publicidad.
* Varias oportunidades iniciales con `CustomMarkerOpportunityGenerator`.
* Un nuevo modo de señalización de publicidad, `CUSTOM_RANGES`.

  Los anuncios se colocan en función de los datos de Intervalo de tiempo de una fuente externa, como un archivo JSON.
