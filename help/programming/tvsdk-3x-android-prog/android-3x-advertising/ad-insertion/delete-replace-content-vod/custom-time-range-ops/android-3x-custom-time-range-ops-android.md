---
description: La clase CustomRangeMetadata identifica diferentes tipos de intervalos de tiempo en una marca de flujo de VOD, que se eliminan y reemplazan. Para cada uno de estos tipos de intervalos de tiempo personalizados, puede realizar las operaciones correspondientes, incluida la eliminación y el reemplazo del contenido de la publicidad.
title: Operaciones de intervalos de tiempo personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Operaciones de intervalo de tiempo personalizado {#custom-time-range-operations}

La clase CustomRangeMetadata identifica diferentes tipos de intervalos de tiempo en un flujo de VOD: marcar, eliminar y reemplazar. Para cada uno de estos tipos de intervalos de tiempo personalizados, puede realizar las operaciones correspondientes, incluida la eliminación y el reemplazo del contenido de la publicidad.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

Para la eliminación y sustitución de anuncios, TVSDK utiliza los siguientes modos *de operación de intervalo de tiempo personalizado*:

* **** MARKTeste modo se denominaba marcadores de anuncio personalizados en versiones anteriores de TVSDK. El modo marca las horas de inicio y finalización de los anuncios que ya se han colocado en el flujo de VOD. Cuando hay marcadores de intervalo de tiempo de tipo `MARK` en el flujo, `CustomMarkerOpportunityGenerator` genera una colocación inicial de `Mode.MARK` y la resuelve `CustomRangeResolver`. No se insertan anuncios.

* **** DELETEFo los intervalos de  `DELETE` tiempo,  `placementInformation` se crea una inicial  `Mode.DELETE` de tipo y se resuelve mediante  `CustomRangeResolver`. `DeleteRangeTimelineOperation` define los intervalos que se eliminarán de la cronología y TVSDK utiliza  `removeByLocalTime` de la API del motor de vídeo de Adobe (AVE) para completar esta operación. Si hay rangos de DELETE y metadatos de toma de decisiones de anuncios de Adobe Primetime, los rangos se eliminan primero y, a continuación, `AuditudeResolver` resuelve los anuncios utilizando el flujo de trabajo típico de Adobe Primetime ad decisioning.

* **** REEMPLAZARo intervalos de  `REPLACE` tiempo,  `placementInformations` se crean dos iniciales, uno  `Mode.DELETE` y uno  `Mode.REPLACE`. `CustomRangeResolver` elimina primero los intervalos de tiempo y, a continuación,  `AuditudeResolver` inserta los anuncios del especificado  `replaceDuration` en la cronología. Si no se especifica ningún `replaceDuration`, el servidor determina qué se debe insertar.

Para admitir estas operaciones personalizadas de intervalo de tiempo, TVSDK proporciona lo siguiente:

* Varios solucionadores de contenido

   Un flujo puede tener varios resoltores de contenido en función del modo de señalización de publicidad y los metadatos de publicidad. El comportamiento cambia con diferentes combinaciones de modos de señalización de publicidad y metadatos de publicidad.
* Varias oportunidades iniciales que utilizan `CustomMarkerOpportunityGenerator`.
* Un nuevo modo de señalización de anuncio, `CUSTOM_RANGES`.

   Los anuncios se colocan en función de los datos del intervalo de tiempo procedentes de un origen externo, como un archivo JSON.