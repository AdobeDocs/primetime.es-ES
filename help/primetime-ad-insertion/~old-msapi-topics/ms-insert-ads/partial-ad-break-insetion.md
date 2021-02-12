---
description: La función Inserción parcial de pausa publicitaria (PABI) imita una experiencia similar a la de un televisor, en la que si el usuario se une a un flujo en directo dentro de un salto de rollover, se muestran al usuario anuncios en versión intermedia en lugar de un anuncio previo o una pizarra.
seo-description: La función Inserción parcial de pausa publicitaria (PABI) imita una experiencia similar a la de un televisor, en la que si el usuario se une a un flujo en directo dentro de un salto de rollover, se muestran al usuario anuncios en versión intermedia en lugar de un anuncio previo o una pizarra.
seo-title: Inserción parcial de pausa publicitaria
title: Inserción parcial de pausa publicitaria
uuid: a0c1ae34-0f8d-4401-97fe-45a2ea40d08d
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Inserción parcial de pausa publicitaria {#partial-ad-break-insertion}

La función Inserción parcial de pausa publicitaria (PABI) imita una experiencia similar a la de un televisor, en la que si el usuario se une a un flujo en directo dentro de un salto de rollover, se muestran al usuario anuncios en versión intermedia en lugar de un anuncio previo o una pizarra.

Cuando el servidor de publicidad devuelve anuncios preliminares para un flujo en directo, el servidor de manifiesto inserta el salto de anuncio previo antes del punto de lanzamiento e inserta la etiqueta EXT-X-INICIO con su valor TIMEOFFSET que apunta al inicio de la pausa publicitaria previa. Este comportamiento predeterminado garantiza que se reproduzca toda la pausa publicitaria previa antes del contenido en el punto activo. Si un usuario se une a un flujo cuando el punto de lanzamiento está cerca de una pausa publicitaria media, se le mostrará la pausa publicitaria previa antes de la pausa publicitaria media en el punto de lanzamiento.

La función PABI indica al servidor de manifiesto que ignore la pausa publicitaria previa y defina el valor EXT-X-INICIO:TIMEOFFSET al principio del anuncio intermedio presente en el punto de lanzamiento. Esto garantiza que el usuario vea todo el anuncio intermedio que se está reproduciendo en el punto de lanzamiento sin tener que realizar la vista de la pausa publicitaria previa.

>[!NOTE]
>
>Esta funcionalidad solo está disponible para flujos en directo. El servidor de manifiesto inserta el salto de anuncio previo sobre la lista de reproducción de VOD de forma predeterminada.

>[!NOTE]
>
>Para habilitar PABI, deberá especificar [consulta_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) en la dirección URL de arranque.

>[!NOTE]
>
>El [EXT-X-INICIO](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) es una etiqueta HLS estándar que indica un punto de partida preferido dentro de la lista de reproducción.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Utilice el seguimiento de cliente porque el cliente tiene más control sobre la activación de las señalizaciones de seguimiento.
* Los saltos parciales de publicidad solo deben usarse con el modo de seguimiento del lado del servidor si el reproductor admite EXT-X-INICIO.