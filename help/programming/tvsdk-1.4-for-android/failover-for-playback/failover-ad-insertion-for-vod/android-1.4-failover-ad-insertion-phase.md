---
description: TVSDK inserta el contenido alternativo (anuncios) en la cronología que corresponde al contenido principal.
title: Fase de inserción de publicidad
exl-id: bad246e9-ff2b-4584-a320-826385bb0e6d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Fase de inserción de publicidad{#ad-insertion-phase}

TVSDK inserta el contenido alternativo (anuncios) en la cronología que corresponde al contenido principal.

Cuando se completa la fase de resolución de anuncios, TVSDK tiene una lista ordenada de recursos publicitarios agrupados en pausas publicitarias. Cada pausa publicitaria se coloca en la cronología del contenido principal mediante un valor de tiempo de inicio que se expresa en milisegundos (ms). Cada anuncio de una pausa publicitaria tiene una propiedad duration que también se expresa en ms. Los anuncios de una pausa publicitaria se encadenan uno tras otro. Como resultado, la duración de una pausa publicitaria es igual a la suma de las duraciones de los anuncios individuales que se componen.

La conmutación por error puede producirse en esta fase con conflictos que pueden producirse en la cronología durante la inserción del anuncio. Para combinaciones específicas de valores de tiempo de inicio/duración de pausa publicitaria, los segmentos de publicidad pueden superponerse. La superposición se produce cuando la última parte de una pausa publicitaria se cruza con el principio del primer anuncio en la siguiente pausa publicitaria. En estas situaciones, TVSDK descarta la pausa publicitaria posterior y continúa el proceso de inserción de publicidad con el siguiente elemento de la lista hasta que se insertan o descartan todas las pausas publicitarias.

TVSDK envía una notificación de advertencia sobre el error y continúa el procesamiento.
