---
description: La clase CustomRangeMetadata identifica diferentes tipos de intervalos de tiempo en una marca de flujo de VOD, eliminación y reemplazo. Para cada uno de estos tipos de intervalo de tiempo personalizado, puede realizar las operaciones correspondientes, incluida la eliminación y sustitución del contenido de la publicidad.
seo-description: La clase CustomRangeMetadata identifica diferentes tipos de intervalos de tiempo en una marca de flujo de VOD, eliminación y reemplazo. Para cada uno de estos tipos de intervalo de tiempo personalizado, puede realizar las operaciones correspondientes, incluida la eliminación y sustitución del contenido de la publicidad.
seo-title: Operaciones de intervalo de tiempo personalizado
title: Operaciones de intervalo de tiempo personalizado
uuid: e9c6a135-124e-44d4-adf2-dc9d671e2483
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Información general {#custom-time-range-operations}

La clase CustomRangeMetadata identifica diferentes tipos de intervalos de tiempo en un flujo VOD: marcar, eliminar y reemplazar. Para cada uno de estos tipos de intervalo de tiempo personalizado, puede realizar las operaciones correspondientes, incluida la eliminación y sustitución del contenido de la publicidad.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

Para la eliminación y sustitución de publicidades, TVSDK utiliza los siguientes modos *de operación de intervalo de tiempo personalizado*:

* **** MARKTeste modo se denominaba marcadores de publicidad personalizados en versiones anteriores de TVSDK. El modo marca las horas de inicio y finalización de las publicidades que ya se han colocado en el flujo de VOD. Cuando hay marcadores de intervalo de tiempo de tipo `MARK` en el flujo, `CustomMarkerOpportunityGenerator` genera una ubicación inicial de `Mode.MARK` y se resuelve mediante `CustomRangeResolver`. No se insertan publicidades.

* **** DELETEFo intervalos de  `DELETE` tiempo,  `placementInformation` se crea y se resuelve un tipo inicial  `Mode.DELETE` de  `CustomRangeResolver`. `DeleteRangeTimelineOperation` define los intervalos que se deben eliminar de la línea de tiempo y TVSDK utiliza  `removeByLocalTime` de la API del motor de vídeo de Adobe (AVE) para completar esta operación. Si hay rangos de DELETE y metadatos de decisiones de anuncios de Adobe Primetime, primero se eliminan los rangos y, a continuación, `AuditudeResolver` resuelve las publicidades utilizando el flujo de trabajo típico de Adobe Primetime de decisiones de anuncios.

* **** REEMPLAZOo intervalos de  `REPLACE` tiempo,  `placementInformations` se crean dos intervalos iniciales, uno  `Mode.DELETE` y uno  `Mode.REPLACE`. `CustomRangeResolver` elimina primero los intervalos de tiempo y, a continuación,  `AuditudeResolver` inserta las publicidades del valor especificado  `replaceDuration` en la línea de tiempo. Si no se especifica `replaceDuration`, el servidor determina qué insertar.

Para admitir estas operaciones de intervalo de tiempo personalizado, TVSDK proporciona lo siguiente:

* Resoluciones de varios contenidos

   Un flujo puede tener varios resueltores de contenido en función del modo de señalización de publicidad y los metadatos de anuncio. El comportamiento cambia con diferentes combinaciones de modos de señalización de publicidad y metadatos de publicidad.
* Varias oportunidades iniciales que utilizan `CustomMarkerOpportunityGenerator`.
* Un nuevo modo de señalización de publicidad, `CUSTOM_RANGES`.

   Las publicidades se colocan en función de los datos del intervalo de tiempo de un origen externo, como un archivo JSON.

