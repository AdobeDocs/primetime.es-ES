---
description: La cronología de anuncios adecuada para una reproducción del contenido de VOD puede ser inapropiada para las reproducciones posteriores. Puede reemplazar una línea de tiempo de VOD sin cambiar el contenido.
seo-description: La cronología de anuncios adecuada para una reproducción del contenido de VOD puede ser inapropiada para las reproducciones posteriores. Puede reemplazar una línea de tiempo de VOD sin cambiar el contenido.
seo-title: Cambios en VOD
title: Cambios en VOD
uuid: e734aacd-b42e-4c8e-a16a-c7a0739a0492
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Cambios en VOD {#changes-to-vod}

La cronología de anuncios adecuada para una reproducción del contenido de VOD puede ser inapropiada para las reproducciones posteriores. Puede reemplazar una línea de tiempo de VOD sin cambiar el contenido.

Entre las situaciones en las que podría desear reemplazar una línea de tiempo de VOD se incluyen:

* Reemplace las publicidades locales, pero deje las publicidades nacionales durante una ventana C3.
* Reemplace las publicidades quemadas después de que se cierre la ventana C3.
* Reemplace dinámicamente anuncios antiguos de C3 con anuncios nuevos de buena duración.
* Inserte menos publicidades o ninguna.

Puede reemplazar la línea de tiempo de la publicidad enviando una nueva solicitud de inserción de publicidad con el archivo M3U8 original y un valor diferente del parámetro de `pttimeline` consulta.