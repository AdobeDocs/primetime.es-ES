---
description: Puede controlar la visibilidad de los subtítulos. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente.
title: Control de la visibilidad de subtítulos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Control de la visibilidad de subtítulos{#control-closed-caption-visibility}

Puede controlar la visibilidad de los subtítulos. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente.

>[!TIP]
>
>Si cambia qué pista es la actual, el ajuste de visibilidad sigue siendo el mismo.

Si se muestra texto de rótulo cerrado cuando el reproductor entra en modo de búsqueda, el texto deja de mostrarse una vez finalizada la búsqueda. En su lugar, después de unos segundos, TVSDK del explorador muestra el siguiente texto de subtítulo cerrado en el vídeo después de la posición de búsqueda final.

>[!TIP]
>
>Los valores de visibilidad de los subtítulos opcionales se controlan con `MediaPlayer.VISIBLE` y `MediaPlayer.INVISIBLE`.

1. Utilice el `MediaPlayer.ccVisibility` para acceder a la configuración de visibilidad actual de los subtítulos.
