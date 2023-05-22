---
description: La función de inserción parcial de pausa publicitaria (PABI) imita una experiencia similar a una TV en la que, si el usuario se une a una emisión en directo dentro de una pausa durante la emisión, se muestra al usuario anuncios durante la emisión en lugar de anuncios previos a la emisión o pizarra.
title: Inserción de pausa publicitaria parcial
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Inserción de pausa publicitaria parcial {#partial-ad-break-insertion}

La función de inserción parcial de pausa publicitaria (PABI) imita una experiencia similar a una TV en la que, si el usuario se une a una emisión en directo dentro de una pausa durante la emisión, se muestra al usuario anuncios durante la emisión en lugar de anuncios previos a la emisión o pizarra.

Cuando el servidor de publicidad devuelve anuncios previos a la emisión de una emisión en directo, el servidor de manifiesto insertará la pausa para anuncios previos a la emisión antes del punto de emisión e insertará la etiqueta EXT-X-START con su valor TIMEOFFSET que señala al inicio de la pausa publicitaria previa a la emisión. Este comportamiento predeterminado garantiza que toda la pausa publicitaria del anuncio previo a la emisión se reproduzca antes que el contenido en el punto en directo. Si un usuario se une a una emisión de flujo cuando el punto de emisión está cerca de una pausa publicitaria en la emisión, se mostrará la pausa publicitaria en la emisión antes de la pausa publicitaria en la emisión en el punto de emisión.

La función PABI indica al servidor de manifiesto que ignore la pausa publicitaria del anuncio previo a la emisión y que establezca el valor EXT-X-START:TIMEOFFSET al principio del anuncio durante la emisión presente en el punto activo. Esto garantiza que el usuario vea todo el anuncio mid-roll que se está reproduciendo en el punto en directo sin tener que ver la pausa publicitaria pre-roll.

>[!NOTE]
>
>Esta funcionalidad solo está disponible para emisiones en directo. El servidor de manifiesto inserta el salto de anuncio previo a la emisión sobre la lista de reproducción de VOD de forma predeterminada.

>[!NOTE]
>
>Para habilitar PABI, deberá especificar la variable [query_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) en la URL de bootstrap.

>[!NOTE]
>
>El [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) es una etiqueta HLS estándar que indica un punto de partida preferido dentro de la lista de reproducción.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Utilice el seguimiento del lado del cliente porque el cliente tiene más control sobre la activación de señalizaciones de seguimiento.
* Las pausas publicitarias parciales solo deben utilizarse con el modo de seguimiento del lado del servidor si el reproductor es compatible con EXT-X-START.