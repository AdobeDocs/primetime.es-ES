---
description: La función Inserción parcial de pausa publicitaria (PABI) imita una experiencia similar a una de TV en la que si el usuario se une a un flujo en directo dentro de una pausa mid-roll, se muestran anuncios mid-roll al usuario, en lugar de un anuncio pre-roll o una pizarra.
title: Inserción parcial de pausa publicitaria
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Inserción parcial de desglose de anuncios {#partial-ad-break-insertion}

La función Inserción parcial de pausa publicitaria (PABI) imita una experiencia similar a una de TV en la que si el usuario se une a un flujo en directo dentro de una pausa mid-roll, se muestran anuncios mid-roll al usuario, en lugar de un anuncio pre-roll o una pizarra.

Cuando el servidor de publicidad devuelva anuncios previos a la emisión para un flujo en directo, el servidor de manifiestos inyectará la pausa publicitaria previa a la emisión antes del punto en directo e insertará la etiqueta EXT-X-START con su valor TIMEOFFSET señalando al inicio de la pausa publicitaria pre-roll. Este comportamiento predeterminado garantiza que se reproduzca toda la pausa publicitaria pre-roll antes del contenido en el punto de lanzamiento. Si un usuario se une a un flujo cuando el punto de lanzamiento está cerca de una pausa publicitaria mid-roll, se mostrará al usuario la pausa publicitaria pre-roll antes de la pausa publicitaria mid-roll en el punto de lanzamiento.

La función PABI indica al servidor de manifiesto que ignore la pausa publicitaria pre-roll y que establezca el valor EXT-X-START:TIMEOFFSET al principio del anuncio mid-roll presente en el punto de lanzamiento. Esto garantiza que el usuario vea todo el anuncio mid-roll reproduciendo actualmente en el punto de lanzamiento sin tener que ver la pausa publicitaria pre-roll.

>[!NOTE]
>
>Esta funcionalidad solo está disponible para transmisiones en directo. El servidor de manifiesto inserta el salto de anuncio previo a la emisión sobre la lista de reproducción de VOD de forma predeterminada.

>[!NOTE]
>
>Para habilitar PABI, deberá especificar [query_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) en la URL de arranque.

>[!NOTE]
>
>El [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) es una etiqueta HLS estándar que indica un punto de partida preferido dentro de la lista de reproducción.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Utilice el seguimiento del lado del cliente porque este tiene más control sobre la activación de señalizaciones de seguimiento.
* Las pausas publicitarias parciales solo deben usarse con el modo de seguimiento del lado del servidor si el reproductor admite EXT-X-START.