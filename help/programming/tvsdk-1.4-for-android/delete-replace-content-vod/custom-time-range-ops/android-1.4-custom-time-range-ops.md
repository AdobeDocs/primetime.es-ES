---
description: TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos de VOD.
title: Operaciones de intervalos de tiempo personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Operaciones de intervalo de tiempo personalizado {#custom-time-range-operations}

TVSDK admite la eliminación y sustitución programáticas de contenido de publicidad en flujos de VOD.

La función de eliminar y reemplazar amplía la función de marcadores de anuncios personalizados. Los marcadores de anuncios personalizados marcan secciones del contenido principal como períodos de contenido relacionado con la publicidad. Además de marcar estos intervalos de tiempo, también puede eliminar y reemplazar intervalos de tiempo.

La eliminación y el reemplazo de anuncios se implementan con `TimeRange` elementos que identifican diferentes tipos de intervalos de tiempo en un flujo de VOD: marcar, eliminar y reemplazar. Para cada uno de estos tipos de intervalos de tiempo personalizados, puede realizar las operaciones correspondientes, incluida la eliminación y el reemplazo del contenido de la publicidad.

Para la eliminación y sustitución de anuncios, TVSDK utiliza los siguientes modos *de operación de intervalo de tiempo personalizado*:

* **MARK**
 (estos se denominaban marcadores de anuncio personalizados en versiones anteriores de TVSDK). Marca las horas de inicio y finalización de los anuncios que ya se han colocado en el flujo de VOD. Cuando hay marcadores de intervalo de tiempo del tipo MARK en el flujo, una colocación inicial de 
`Mode.MARK` la genera y resuelve el  `CustomAdMarkersContentResolver`. No se insertan anuncios.

* ****
ELIMINARo intervalos de tiempo del DELETE, una 
`placementInformation` del tipo  `Mode.DELETE` se crea y resuelve mediante el  `DeleteContentResolver`. `ContentRemoval` es un nuevo  `timelineOperation` que define los intervalos que se eliminarán de la cronología. TVSDK utiliza `removeByLocalTime` de la API del motor de vídeo de Adobe (AVE) para facilitar esa operación. Si hay intervalos de DELETE y metadatos de toma de decisiones de anuncios de Adobe Primetime (anteriormente conocidos como Auditude), primero se eliminan los intervalos, entonces `AuditudeResolver` resuelve los anuncios utilizando el flujo de trabajo normal de Adobe Primetime ad decisioning.

* ****
REEMPLAZARo REEMPLAZAR intervalos de tiempo, dos 
`placementInformations` se crean, uno  `Mode.DELETE` y uno  `Mode.REPLACE`. El `DeleteContentResolver` elimina primero los intervalos de tiempo y luego el `AuditudeResolver` inserta los anuncios del `replaceDuration` especificado en la cronología. Si no se especifica ningún `replaceDuration`, el servidor determina qué se debe insertar.

Para admitir estas operaciones personalizadas de intervalo de tiempo, TVSDK proporciona lo siguiente:

* Varios solucionadores de contenido

   Un flujo puede tener varios resoltores de contenido en función del modo de señalización de publicidad y los metadatos de publicidad. El comportamiento cambia con diferentes combinaciones de modos de señalización de publicidad y metadatos de publicidad.
* Varios `PlacementInformations` iniciales El `DefaultMediaPlayer` crea una lista de `PlacementInformations` iniciales en función del modo de señalización de anuncios y los metadatos de publicidad que resolverá el `MediaPlayerClient`.

* Nuevo modo de señalización de publicidad: Intervalos de tiempo personalizados

   Los anuncios se colocan en función de los datos del intervalo de tiempo procedentes de un origen externo (como un archivo JSON).