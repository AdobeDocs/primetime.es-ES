---
description: La cronología del anuncio adecuada para una reproducción del contenido de VOD puede ser inapropiada para reproducciones posteriores. Puede reemplazar una cronología de VOD sin cambiar el contenido.
title: Cambios en VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Cambios en VOD {#changes-to-vod}

La cronología del anuncio adecuada para una reproducción del contenido de VOD puede ser inapropiada para reproducciones posteriores. Puede reemplazar una cronología de VOD sin cambiar el contenido.

Las situaciones en las que puede que desee reemplazar una cronología de VOD incluyen:

* Reemplace los anuncios locales, pero deje los anuncios nacionales durante una ventana C3.
* Reemplace los anuncios quemados después de que se cierre la ventana C3.
* Reemplace dinámicamente los anuncios antiguos de C3 con anuncios más nuevos de buena duración.
* Inserte menos anuncios o ninguno en absoluto.

Puede reemplazar la cronología de la publicidad enviando una nueva solicitud de inserción de publicidad con el archivo M3U8 original y un valor diferente del parámetro de consulta `pttimeline`.