---
description: La clase CustomRangeMetadata identifica diferentes tipos de intervalos de tiempo en una marca de flujo de VOD, eliminación y reemplazo. Para cada uno de estos tipos de intervalo de tiempo personalizado, puede realizar las operaciones correspondientes, incluida la eliminación y sustitución del contenido de la publicidad.
seo-description: La clase CustomRangeMetadata identifica diferentes tipos de intervalos de tiempo en una marca de flujo de VOD, eliminación y reemplazo. Para cada uno de estos tipos de intervalo de tiempo personalizado, puede realizar las operaciones correspondientes, incluida la eliminación y sustitución del contenido de la publicidad.
seo-title: Operaciones de intervalo de tiempo personalizado
title: Operaciones de intervalo de tiempo personalizado
uuid: eadd4d8d-0e03-40ca-ae3b-eede82bf2df8
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Operaciones de intervalo de tiempo personalizado {#custom-time-range-operations}

La clase CustomRangeMetadata identifica diferentes tipos de intervalos de tiempo en un flujo VOD: marcar, eliminar y reemplazar. Para cada uno de estos tipos de intervalo de tiempo personalizado, puede realizar las operaciones correspondientes, incluida la eliminación y sustitución del contenido de la publicidad.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

Para la eliminación y sustitución de publicidades, TVSDK utiliza los siguientes modos de operación *de intervalo de tiempo* personalizados:

* **MARCA** Este modo se denominaba marcadores de publicidad personalizados en versiones anteriores de TVSDK. El modo marca las horas de inicio y finalización de las publicidades que ya se han colocado en el flujo de VOD. Cuando hay marcadores de intervalo de tiempo de tipo `MARK` en el flujo, `Mode.MARK` se genera una colocación inicial de `CustomMarkerOpportunityGenerator` y se resuelve mediante `CustomRangeResolver`. No se insertan publicidades.

* **ELIMINAR** Para `DELETE` intervalos de tiempo, se crea una inicial `placementInformation` de tipo `Mode.DELETE` y se resuelve mediante `CustomRangeResolver`. `DeleteRangeTimelineOperation` define los intervalos que se deben eliminar de la línea de tiempo y TVSDK utiliza `removeByLocalTime` la API de motor de vídeo de Adobe (AVE) para completar esta operación. Si hay intervalos ELIMINADOS y metadatos de toma de decisiones de anuncios de Adobe Primetime, primero se eliminan los intervalos y, a continuación, `AuditudeResolver` se resuelven las publicidades utilizando el flujo de trabajo típico de toma de decisiones y de Adobe Primetime.

* **REEMPLAZAR** Para `REPLACE` intervalos de tiempo, se crean dos `placementInformations` iniciales, uno `Mode.DELETE` y otro `Mode.REPLACE`. `CustomRangeResolver` elimina primero los intervalos de tiempo y, a continuación, `AuditudeResolver` inserta las publicidades de la `replaceDuration` línea de tiempo especificada. Si no `replaceDuration` se especifica ninguno, el servidor determina qué se va a insertar.

Para admitir estas operaciones de intervalo de tiempo personalizado, TVSDK proporciona lo siguiente:

* Resoluciones de varios contenidos

   Un flujo puede tener varios resueltores de contenido en función del modo de señalización de publicidad y los metadatos de anuncio. El comportamiento cambia con diferentes combinaciones de modos de señalización de publicidad y metadatos de publicidad.
* Varias oportunidades iniciales que utilizan `CustomMarkerOpportunityGenerator`.
* Un nuevo modo de señalización de publicidad, `CUSTOM_RANGES`.

   Las publicidades se colocan en función de los datos del intervalo de tiempo de un origen externo, como un archivo JSON.