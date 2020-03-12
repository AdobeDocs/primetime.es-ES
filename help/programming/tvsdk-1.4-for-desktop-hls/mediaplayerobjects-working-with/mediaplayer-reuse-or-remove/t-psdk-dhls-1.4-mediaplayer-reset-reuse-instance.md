---
description: Cuando se restablece una instancia de MediaPlayer, se devuelve a su estado IDLE no inicializado tal como se define en MediaPlayerStatus.
seo-description: Cuando se restablece una instancia de MediaPlayer, se devuelve a su estado IDLE no inicializado tal como se define en MediaPlayerStatus.
seo-title: Restablecer o reutilizar una instancia de MediaPlayer
title: Restablecer o reutilizar una instancia de MediaPlayer
uuid: b376096b-0aed-4ac2-96e5-e30a4eaf742e
translation-type: tm+mt
source-git-commit: c547002eb8946f8ccc5a79d0836f3f814e823b97

---


# Restablecer o reutilizar una instancia de MediaPlayer{#reset-or-reuse-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

Cuando se restablece una instancia de MediaPlayer, se devuelve a su estado IDLE no inicializado tal como se define en MediaPlayerStatus.

Esta operación resulta útil en los siguientes casos:

* Desea reutilizar una `MediaPlayer` instancia, pero debe cargar un nuevo `MediaResource` (contenido de vídeo) y reemplazar la instancia anterior.

   Restablecer le permite reutilizar la `MediaPlayer` instancia sin la sobrecarga de liberar recursos, volver a crearlos `MediaPlayer`y reasignar recursos. Los métodos `replaceCurrentItem` y `replaceCurrentResource` realizan automáticamente estos pasos sin tener que llamar al método reset.

* Cuando el `MediaPlayer` tiene un estado ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado ERROR.

1. Llamada `reset` para devolver la `MediaPlayer` instancia a su estado no inicializado:

   ```
   function reset():void; 
   ```

1. Use `MediaPlayer.replaceCurrentItem` o `MediaPlayer.replaceCurrentResource` para cargar otro `MediaResource`.

   >[!TIP]
   >
   >Para borrar un error, cargue lo mismo `MediaResource`.

1. Cuando reciba el `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con el `PREPARED` estado, inicie la reproducción.
