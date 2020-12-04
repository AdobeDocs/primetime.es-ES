---
description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.
seo-description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.
seo-title: Operaciones de intervalo de tiempo personalizado
title: Operaciones de intervalo de tiempo personalizado
uuid: e04af786-8dac-41a6-8406-f2ca04f612a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Operaciones de intervalo de tiempo personalizado {#custom-time-range-operations}

TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos VOD.

La función Eliminar y reemplazar amplía la función de marcadores de publicidad personalizados. Los marcadores de publicidad personalizados marcan secciones del contenido principal como períodos de contenido relacionados con la publicidad. Además de marcar estos intervalos de tiempo, también puede eliminar y reemplazar dichos intervalos.

La eliminación y sustitución de publicidades se implementan con `TimeRange` elementos que identifican diferentes tipos de intervalos de tiempo en un flujo de VOD: marcar, eliminar y reemplazar. Para cada uno de estos tipos de intervalo de tiempo personalizado, puede realizar las operaciones correspondientes, incluida la eliminación y sustitución del contenido de la publicidad.

Para la eliminación y sustitución de publicidades, TVSDK utiliza los siguientes modos *de operación de intervalo de tiempo personalizado*:

* **MARK**
(Estos se denominaban marcadores de publicidad personalizados en versiones anteriores de TVSDK). Marcan las horas de inicio y finalización para las publicidades que ya se colocan en el flujo de VOD. Cuando hay marcadores de intervalo de tiempo de tipo MARK en el flujo, se coloca una colocación inicial de 
`Mode.MARK` es generado y resuelto por el  `CustomAdMarkersContentResolver`. No se insertan publicidades.

* ****
DELETEFo intervalos de tiempo del DELETE, un 
`placementInformation` del tipo  `Mode.DELETE` se crea y se resuelve mediante el  `DeleteContentResolver`. `ContentRemoval` es un nuevo  `timelineOperation` que define los intervalos que se eliminarán de la línea de tiempo. TVSDK utiliza `removeByLocalTime` de la API del motor de vídeo de Adobe (AVE) para facilitar esa operación. Si hay rangos de DELETE y metadatos de decisiones de anuncios de Adobe Primetime (anteriormente conocidos como Auditude), primero se eliminan los rangos y, a continuación, `AuditudeResolver` resuelve las publicidades mediante el flujo de trabajo normal de Adobe Primetime y de decisiones de anuncios.

* ****
REEMPLAZARo REEMPLAZAR intervalos de tiempo, dos 
`placementInformations` se crean, uno  `Mode.DELETE` y uno  `Mode.REPLACE`. El `DeleteContentResolver` elimina primero los intervalos de tiempo y luego el `AuditudeResolver` inserta publicidades del `replaceDuration` especificado en la línea de tiempo. Si no se especifica `replaceDuration`, el servidor determina qué insertar.

Para admitir estas operaciones de intervalo de tiempo personalizado, TVSDK proporciona lo siguiente:

* Resoluciones de varios contenidos

   Un flujo puede tener varios resueltores de contenido en función del modo de señalización de publicidad y los metadatos de anuncio. El comportamiento cambia con diferentes combinaciones de modos de señalización de publicidad y metadatos de publicidad.
* Varios `PlacementInformations` iniciales El `DefaultMediaPlayer` crea una lista de `PlacementInformations` inicial basada en el modo de señalización de publicidad y los metadatos de publicidad que se resolverán con el `MediaPlayerClient`.

* Nuevo modo de señalización de publicidad: Intervalos de tiempo personalizados

   Las publicidades se colocan en función de los datos del intervalo de tiempo de un origen externo (como un archivo JSON).