---
description: Puede controlar la visibilidad de los subtítulos cerrados. Cuando se ha habilitado la visibilidad, se muestra la pista seleccionada actualmente. Si cambia la pista que está actualizada, la configuración de visibilidad seguirá siendo la misma.
title: Control de la visibilidad de los subtítulos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 1%

---


# Control de la visibilidad de los subtítulos {#control-closed-caption-visibility}

Puede controlar la visibilidad de los subtítulos cerrados. Cuando se ha habilitado la visibilidad, se muestra la pista seleccionada actualmente. Si cambia la pista que está actualizada, la configuración de visibilidad seguirá siendo la misma.

>[!TIP]
>
>Si el texto del subtítulo se muestra cuando el reproductor entra en el modo de búsqueda, el texto ya no se muestra una vez finalizada la búsqueda. En su lugar, después de unos segundos, TVSDK muestra el siguiente texto de subtítulo cerrado en el vídeo después de la posición de búsqueda final.
>
>Los valores de visibilidad para los subtítulos cerrados se definen en `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. Espere a que `MediaPlayer` esté en al menos el estado PREPARADO. Para obtener más información, consulte [Espera a un estado válido](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-state-prepared-wait-for.md).

1. Para obtener la configuración de visibilidad actual para los subtítulos cerrados, utilice el método getter en `MediaPlayer`, que devuelve un valor de visibilidad.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. Para cambiar la visibilidad de los subtítulos cerrados, utilice el método setter, pasando un valor de visibilidad de `MediaPlayer.Visibility`.

   Por ejemplo:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
