---
description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.
seo-description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.
seo-title: Operaciones de intervalo de tiempo personalizado
title: Operaciones de intervalo de tiempo personalizado
uuid: e04af786-8dac-41a6-8406-f2ca04f612a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Operaciones de intervalo de tiempo personalizado {#custom-time-range-operations}

TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.

La función Eliminar y reemplazar amplía la función de marcadores de publicidad personalizados. Los marcadores de publicidad personalizados marcan secciones del contenido principal como períodos de contenido relacionados con la publicidad. Además de marcar estos intervalos de tiempo, también puede eliminar y reemplazar dichos intervalos.

La eliminación y sustitución de publicidades se implementan con `TimeRange` elementos que identifican diferentes tipos de intervalos de tiempo en un flujo de VOD: marcar, eliminar y reemplazar. Para cada uno de estos tipos de intervalo de tiempo personalizado, puede realizar las operaciones correspondientes, incluida la eliminación y sustitución del contenido de la publicidad.

Para la eliminación y sustitución de publicidades, TVSDK utiliza los siguientes modos de operación *de intervalo de tiempo* personalizados:

* **MARK**(Estos se denominaban marcadores de publicidad personalizados en versiones anteriores de TVSDK). Marcan las horas de inicio y finalización para las publicidades que ya se colocan en el flujo de VOD. Cuando hay marcadores de intervalo de tiempo de tipo MARK en el flujo, `Mode.MARK` se genera y se resuelve una colocación inicial del `CustomAdMarkersContentResolver`. No se insertan publicidades.

* **ELIMINAR** Para ELIMINAR intervalos de tiempo, se crea una inicial `placementInformation` de tipo `Mode.DELETE` y se resuelve con la correspondiente `DeleteContentResolver`. `ContentRemoval` es un nuevo `timelineOperation` que define los intervalos que se eliminarán de la línea de tiempo. TVSDK utiliza `removeByLocalTime` la API de motor de vídeo de Adobe (AVE) para facilitar esa operación. Si hay intervalos ELIMINADOS y metadatos de decisiones de anuncios de Adobe Primetime (anteriormente conocidos como Auditude), los intervalos se eliminan primero y, a continuación, `AuditudeResolver` resuelven las publicidades utilizando el flujo de trabajo normal de decisiones de anuncios de Adobe Primetime.

* **REEMPLAZAR** Para los intervalos de tiempo de REEMPLAZO, `placementInformations` se crean dos iniciales, uno `Mode.DELETE` y otro `Mode.REPLACE`. El `DeleteContentResolver` elimina primero los intervalos de tiempo y, a continuación, `AuditudeResolver` inserta anuncios de los especificados `replaceDuration` en la línea de tiempo. Si no `replaceDuration` se especifica ninguno, el servidor determina qué se va a insertar.

Para admitir estas operaciones de intervalo de tiempo personalizado, TVSDK proporciona lo siguiente:

* Resoluciones de varios contenidos

   Un flujo puede tener varios resueltores de contenido en función del modo de señalización de publicidad y los metadatos de anuncio. El comportamiento cambia con diferentes combinaciones de modos de señalización de publicidad y metadatos de publicidad.
* Varias iniciales `PlacementInformations` El `DefaultMediaPlayer` crea una lista de las iniciales `PlacementInformations` en función del modo de señalización de publicidad y los metadatos de publicidad que el `MediaPlayerClient`resuelva.

* Nuevo modo de señalización de publicidad: Intervalos de tiempo personalizados

   Las publicidades se colocan en función de los datos del intervalo de tiempo de un origen externo (como un archivo JSON).