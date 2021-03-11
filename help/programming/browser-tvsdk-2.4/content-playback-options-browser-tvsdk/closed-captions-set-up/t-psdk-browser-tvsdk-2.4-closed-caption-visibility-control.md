---
description: Puede controlar la visibilidad de los subtítulos cerrados. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente.
title: Control de la visibilidad de los subtítulos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Control de la visibilidad de los subtítulos {#control-closed-caption-visibility}

Puede controlar la visibilidad de los subtítulos cerrados. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente.

>[!TIP]
>
>Si cambia la pista que está actualizada, la configuración de visibilidad seguirá siendo la misma.

Si se muestra texto de rótulo cerrado cuando el reproductor entra en el modo de búsqueda, el texto ya no se muestra una vez finalizada la búsqueda. En su lugar, después de unos segundos, el SDK de explorador muestra el siguiente texto de subtítulo cerrado en el vídeo después de la posición de búsqueda final.

>[!TIP]
>
>Los valores de visibilidad de los subtítulos cerrados se controlan con `MediaPlayer.VISIBLE` y `MediaPlayer.INVISIBLE`.

1. Utilice la propiedad `MediaPlayer.ccVisibility` para acceder a la configuración de visibilidad actual de los subtítulos.

