---
description: Puede controlar la visibilidad de los subtítulos. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente. Si cambia qué pista es la actual, el ajuste de visibilidad sigue siendo el mismo.
title: Control de la visibilidad de subtítulos
exl-id: d9428744-1700-4917-b334-d6e0446eaf37
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Información general {#control-closed-caption-visibility}

Puede controlar la visibilidad de los subtítulos. Cuando la visibilidad está activada, se muestra la pista seleccionada actualmente. Si cambia qué pista es la actual, el ajuste de visibilidad sigue siendo el mismo.

>[!TIP]
>
>Si se muestra texto de rótulo cerrado cuando el reproductor entra en modo de búsqueda, el texto ya no se mostrará una vez finalizada la búsqueda. En su lugar, después de unos segundos, TVSDK muestra el siguiente texto de subtítulo cerrado en el vídeo después de la posición de búsqueda final.

>[!NOTE]
>
>Los valores de visibilidad de los subtítulos opcionales se definen en `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. Espere a que MediaPlayer tenga al menos el estado PREPARED (consulte [Esperar a un estado válido](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)).
1. Para obtener la configuración de visibilidad actual de los subtítulos cerrados, utilice el método getter en MediaPlayer, que devuelve un valor de visibilidad.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. Para cambiar la visibilidad de los subtítulos opcionales, utilice el método setter y pase un valor de visibilidad de `MediaPlayer.Visibility`.

   Por ejemplo:

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```
