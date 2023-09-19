---
description: Puede controlar la visibilidad de los subtítulos. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente. Si cambia qué pista es la actual, el ajuste de visibilidad sigue siendo el mismo.
title: Control de la visibilidad de subtítulos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Información general {#control-closed-caption-visibility-overview}

Puede controlar la visibilidad de los subtítulos. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente. Si cambia qué pista es la actual, el ajuste de visibilidad sigue siendo el mismo.

>[!TIP]
>
>Si se muestra texto de rótulo cerrado cuando el reproductor entra en el modo de búsqueda, el texto ya no se mostrará una vez finalizada la búsqueda. En su lugar, después de unos segundos, TVSDK muestra el siguiente texto de subtítulo cerrado en el vídeo después de la posición de búsqueda final.
>
>Los valores de visibilidad de los subtítulos opcionales se definen en `MediaPlayer.Visibility`.
>
>```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```
>

1. Espere a que `MediaPlayer` para que esté al menos en estado PREPARADO.

   Para obtener más información, consulte ui-state-prepared-wait-for .
1. Para obtener la configuración de visibilidad actual de los subtítulos opcionales, utilice el método de captador en `MediaPlayer`, que devuelve un valor de visibilidad.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. Para cambiar la visibilidad de los subtítulos opcionales, utilice el método setter y pase un valor de visibilidad de `MediaPlayer.Visibility`.

   Por ejemplo:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
