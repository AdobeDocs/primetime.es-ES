---
description: TVSDK inserta el contenido alternativo (publicidades) en la línea de tiempo que corresponde al contenido principal.
seo-description: TVSDK inserta el contenido alternativo (publicidades) en la línea de tiempo que corresponde al contenido principal.
seo-title: Fase de inserción de publicidad
title: Fase de inserción de publicidad
uuid: 4a8e9578-6e95-44c0-b045-ae3c20da75e9
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Fase de inserción de publicidad{#ad-insertion-phase}

TVSDK inserta el contenido alternativo (publicidades) en la línea de tiempo que corresponde al contenido principal.

Cuando se completa la fase de resolución de publicidad, TVSDK tiene una lista ordenada de recursos publicitarios que se agrupan en saltos de publicidad. Cada pausa publicitaria se coloca en la línea de tiempo del contenido principal utilizando un valor de tiempo de inicio expresado en milisegundos (ms). Cada publicidad de una pausa publicitaria tiene una propiedad duration que también se expresa en ms. Las publicidades de una pausa publicitaria se encadenan una tras otra. Como resultado, la duración de una pausa publicitaria es igual a la suma de las duraciones de las publicidades compuestas individuales.

La conmutación por error puede ocurrir en esta fase con conflictos que pueden producirse en la línea de tiempo durante la inserción de anuncios. Para combinaciones específicas de valores de tiempo de inicio/duración de desglose de publicidad, los segmentos de publicidad podrían superponerse. La superposición se produce cuando la última parte de una pausa publicitaria se cruza con el principio del primer anuncio en la siguiente pausa publicitaria. En estas situaciones, TVSDK descarta la pausa publicitaria posterior y continúa el proceso de inserción con el siguiente elemento de la lista hasta que se insertan o descarten todos los saltos de publicidad.

TVSDK emite una notificación de advertencia sobre el error y continúa el procesamiento.
