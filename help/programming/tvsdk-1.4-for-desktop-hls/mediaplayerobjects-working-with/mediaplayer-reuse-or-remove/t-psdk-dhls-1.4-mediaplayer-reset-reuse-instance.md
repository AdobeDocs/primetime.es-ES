---
description: Cuando se restablece una instancia de MediaPlayer, se vuelve a su estado IDLE sin inicializar tal como se define en MediaPlayerStatus.
title: Restablecer o reutilizar una instancia de MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# Restablecer o reutilizar una instancia de MediaPlayer{#reset-or-reuse-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

Cuando se restablece una instancia de MediaPlayer, se vuelve a su estado IDLE sin inicializar tal como se define en MediaPlayerStatus.

Esta operación resulta útil en los siguientes casos:

* Desea reutilizar una instancia `MediaPlayer` pero debe cargar un nuevo `MediaResource` (contenido de vídeo) y reemplazar la instancia anterior.

   El restablecimiento le permite reutilizar la instancia `MediaPlayer` sin necesidad de liberar recursos, volver a crear `MediaPlayer` y reasignar recursos. Los métodos `replaceCurrentItem` y `replaceCurrentResource` realizan automáticamente estos pasos sin tener que llamar al método reset.

* Cuando el `MediaPlayer` tiene un estado de ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado de ERROR.

1. Llame a `reset` para devolver la instancia `MediaPlayer` a su estado no inicializado:

   ```
   function reset():void; 
   ```

1. Utilice `MediaPlayer.replaceCurrentItem` o `MediaPlayer.replaceCurrentResource` para cargar otro `MediaResource`.

   >[!TIP]
   >
   >Para borrar un error, cargue el mismo `MediaResource`.

1. Cuando reciba el `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con el estado `PREPARED`, inicie la reproducción.
