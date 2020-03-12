---
description: Puede controlar la visibilidad de los subtítulos opcionales. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente.
seo-description: Puede controlar la visibilidad de los subtítulos opcionales. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente.
seo-title: Control de la visibilidad de los subtítulos opcionales
title: Control de la visibilidad de los subtítulos opcionales
uuid: b161a729-73f3-4019-a95e-013b42779842
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Control de la visibilidad de los subtítulos opcionales{#control-closed-caption-visibility}

Puede controlar la visibilidad de los subtítulos opcionales. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente.

>[!TIP]
>
>Si cambia la pista que está actualizada, la configuración de visibilidad permanece igual.

Si se muestra texto de subtítulos opcionales cuando el reproductor entra en el modo de búsqueda, el texto ya no se muestra una vez finalizada la búsqueda. En su lugar, después de unos segundos, el SDK de TVSDK del explorador muestra el siguiente texto de subtítulos opcionales en el vídeo después de la posición de búsqueda final.

>[!TIP]
>
>Los valores de visibilidad de los subtítulos cerrados se controlan con `MediaPlayer.VISIBLE` y `MediaPlayer.INVISIBLE`.

1. Utilice la propiedad `MediaPlayer.ccVisibility` para acceder a la configuración de visibilidad actual de los subtítulos cerrados.

