---
description: Puede controlar la visibilidad de los subtítulos opcionales. Cuando se ha habilitado la visibilidad, se muestra la pista seleccionada actualmente. Si cambia la pista que está actualizada, la configuración de visibilidad permanece igual.
seo-description: Puede controlar la visibilidad de los subtítulos opcionales. Cuando se ha habilitado la visibilidad, se muestra la pista seleccionada actualmente. Si cambia la pista que está actualizada, la configuración de visibilidad permanece igual.
seo-title: Control de la visibilidad de los subtítulos opcionales
title: Control de la visibilidad de los subtítulos opcionales
uuid: f142e60d-5581-4d1c-9d4d-a4a58ac1b67b
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Control de la visibilidad de los subtítulos opcionales {#control-closed-caption-visibility}

Puede controlar la visibilidad de los subtítulos opcionales. Cuando se ha habilitado la visibilidad, se muestra la pista seleccionada actualmente. Si cambia la pista que está actualizada, la configuración de visibilidad permanece igual.

>[!TIP]
>
>Si se muestra texto de subtítulos opcionales cuando el reproductor entra en el modo de búsqueda, el texto ya no se muestra una vez finalizada la búsqueda. En su lugar, después de unos segundos, TVSDK muestra el siguiente texto de subtítulos opcionales en el vídeo después de la posición de búsqueda final.
>
>Los valores de visibilidad de los subtítulos cerrados se definen en `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. Espere a que el `MediaPlayer` estado esté al menos en el estado PREPARADO. Para obtener más información, consulte [Esperar un estado](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-state-prepared-wait-for.md)válido.

1. Para obtener la configuración de visibilidad actual de los subtítulos cerrados, utilice el método getter en `MediaPlayer`, que devuelve un valor de visibilidad.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. Para cambiar la visibilidad de los subtítulos cerrados, utilice el método setter, pasando un valor de visibilidad de `MediaPlayer.Visibility`.

   Por ejemplo:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
