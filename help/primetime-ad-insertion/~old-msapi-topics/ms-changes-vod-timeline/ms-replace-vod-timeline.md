---
description: La cronología del anuncio apropiada para una reproducción de contenido de VOD puede no ser apropiada para reproducciones posteriores. Puede reemplazar una cronología de VOD sin cambiar el contenido.
title: Cambios en VOD
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# Cambios en VOD {#changes-to-vod}

La cronología del anuncio apropiada para una reproducción de contenido de VOD puede no ser apropiada para reproducciones posteriores. Puede reemplazar una cronología de VOD sin cambiar el contenido.

Las situaciones en las que es posible que desee reemplazar una cronología de VOD incluyen:

* Reemplazar anuncios locales, pero dejar anuncios nacionales durante una ventana C3.
* Reemplace los anuncios quemados después de que se cierre la ventana C3.
* Reemplazar dinámicamente los anuncios antiguos de C3 con anuncios más nuevos de buena duración.
* Inserte menos anuncios o ninguno.

Puede reemplazar la cronología de la publicidad enviando una nueva solicitud de inserción de publicidad con el archivo M3U8 original y un valor diferente de `pttimeline` parámetro de consulta.