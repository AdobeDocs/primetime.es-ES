---
description: TVSDK inserta el contenido alternativo (anuncios) en la cronología que corresponde al contenido principal.
title: Fase de inserción de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Fase de inserción de publicidad{#ad-insertion-phase}

TVSDK inserta el contenido alternativo (anuncios) en la cronología que corresponde al contenido principal.

Cuando finaliza la fase de resolución de anuncios, TVSDK tiene una lista ordenada de recursos publicitarios que se agrupan en pausas publicitarias. Cada pausa publicitaria se coloca en la cronología del contenido principal utilizando un valor de tiempo de inicio expresado en milisegundos (ms). Cada anuncio de una pausa publicitaria tiene una propiedad duration que también se expresa en ms. Los anuncios de una pausa publicitaria se encadenan uno tras otro. Como resultado, la duración de una pausa publicitaria es igual a la suma de las duraciones de los anuncios compuestos individuales.

La conmutación por error puede ocurrir en esta fase con conflictos que podrían producirse en la cronología durante la inserción del anuncio. Para combinaciones específicas de valores de tiempo de inicio/duración de las pausas publicitarias, los segmentos publicitarios podrían superponerse. La superposición se produce cuando la última parte de una pausa publicitaria se cruza con el principio del primer anuncio de la siguiente pausa publicitaria. En estas situaciones, TVSDK descarta la pausa publicitaria posterior y continúa el proceso de inserción con el siguiente elemento de la lista hasta que se insertan o descartan todas las pausas publicitarias.

TVSDK envía una notificación de advertencia sobre el error y continúa con el procesamiento.
