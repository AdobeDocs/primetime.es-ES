---
description: TVSDK admite la eliminación y el reemplazo mediante programación del contenido de anuncios en flujos de VOD.
title: Operaciones de intervalo de tiempo personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Operaciones de intervalo de tiempo personalizadas {#custom-time-range-operations}

TVSDK admite la eliminación y el reemplazo mediante programación del contenido de anuncios en flujos de VOD.

La función Eliminar y reemplazar amplía la función de marcadores de publicidad personalizados. Los marcadores de publicidad personalizados marcan secciones del contenido principal como periodos de contenido relacionados con anuncios. Además de marcar estos intervalos de tiempo, también puede eliminar y reemplazar intervalos de tiempo.

La eliminación y el reemplazo de publicidad se implementan con `TimeRange` elementos que identifican distintos tipos de intervalos de tiempo en un flujo de VOD: marcar, eliminar y reemplazar. Para cada uno de estos tipos de intervalos de tiempo personalizados, puede realizar las operaciones correspondientes, incluida la eliminación y el reemplazo del contenido de la publicidad.

Para eliminar y reemplazar anuncios, TVSDK utiliza lo siguiente *operación de intervalo de tiempo personalizado* modos:

* **MARCAR**
(Estos se denominaban marcadores de anuncios personalizados en versiones anteriores de TVSDK). Marcan las horas de inicio y finalización de los anuncios que ya se han colocado en el flujo de VOD. Cuando hay marcadores de intervalo de tiempo de tipo MARK en la secuencia, una colocación inicial de `Mode.MARK` se genera y resuelve mediante `CustomAdMarkersContentResolver`. No se han insertado anuncios.

* **DELETE**
Para intervalos de tiempo DELETE, una `placementInformation` de tipo `Mode.DELETE` se crea y resuelve mediante el `DeleteContentResolver`. `ContentRemoval` es un nuevo `timelineOperation` que define los rangos que se eliminarán de la cronología. TVSDK utiliza `removeByLocalTime` de la API de Adobe Video Engine (AVE) para facilitar esa operación. Si hay rangos de DELETE y metadatos de Adobe Primetime ad decisioning (anteriormente conocidos como Auditude), los rangos se eliminan primero, luego la variable `AuditudeResolver` resuelve los anuncios mediante el flujo de trabajo normal de Adobe Primetime ad decisioning.

* **REPLACE**
Para los intervalos de tiempo de REEMPLAZO, dos `placementInformations` se crean, uno `Mode.DELETE` y uno `Mode.REPLACE`. El `DeleteContentResolver` elimina primero los intervalos de tiempo y, a continuación, el `AuditudeResolver` inserta anuncios del especificado `replaceDuration` en la cronología. Si no `replaceDuration` se especifica, el servidor determina qué se inserta.

Para admitir estas operaciones de intervalo de tiempo personalizado, TVSDK proporciona lo siguiente:

* Varias resoluciones de contenido

  Un flujo puede tener varias resoluciones de contenido basadas en el modo de señalización de publicidad y los metadatos de publicidad. El comportamiento cambia con diferentes combinaciones de modos de señalización de publicidad y metadatos de publicidad.
* Varias iniciales `PlacementInformations` El `DefaultMediaPlayer` crea una lista de `PlacementInformations` en función del modo de señalización de publicidad y los metadatos de publicidad que debe resolver el `MediaPlayerClient`.

* Nuevo modo de señalización de publicidad: intervalos de tiempo personalizados

  Los anuncios se colocan en función de los datos de Intervalo de tiempo de una fuente externa (como un archivo JSON).
