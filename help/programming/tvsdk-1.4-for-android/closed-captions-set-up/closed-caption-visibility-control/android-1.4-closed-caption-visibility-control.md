---
description: Puede controlar la visibilidad de los subtítulos opcionales. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente. Si cambia la pista que está actualizada, la configuración de visibilidad permanece igual.
seo-description: Puede controlar la visibilidad de los subtítulos opcionales. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente. Si cambia la pista que está actualizada, la configuración de visibilidad permanece igual.
seo-title: Control de la visibilidad de los subtítulos opcionales
title: Control de la visibilidad de los subtítulos opcionales
uuid: 42913347-8158-474e-aa3c-ba4d38baba12
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Información general {#control-closed-caption-visibility}

Puede controlar la visibilidad de los subtítulos opcionales. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente. Si cambia la pista que está actualizada, la configuración de visibilidad permanece igual.

>[!TIP]
>
>Si se muestra texto de subtítulos opcionales cuando el reproductor entra en el modo de búsqueda, el texto ya no se muestra una vez finalizada la búsqueda. En su lugar, después de unos segundos, TVSDK muestra el siguiente texto de subtítulos opcionales en el vídeo después de la posición de búsqueda final.

>[!NOTE]
>
>Los valores de visibilidad de los subtítulos cerrados se definen en `MediaPlayer.Visibility`. >
>
```java>
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```>



1. Espere a que MediaPlayer tenga al menos el estado PREPARADO (consulte [Esperar un estado](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)válido).
1. Para obtener la configuración de visibilidad actual de los subtítulos cerrados, utilice el método getter en MediaPlayer, que devuelve un valor de visibilidad.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. Para cambiar la visibilidad de los subtítulos cerrados, utilice el método setter, pasando un valor de visibilidad de `MediaPlayer.Visibility`.

   Por ejemplo:

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```

