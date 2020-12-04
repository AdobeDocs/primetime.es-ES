---
description: Cuando se restablece una instancia de MediaPlayer, se devuelve a su estado IDLE no inicializado tal como se define en MediaPlayerState.
seo-description: Cuando se restablece una instancia de MediaPlayer, se devuelve a su estado IDLE no inicializado tal como se define en MediaPlayerState.
seo-title: Restablecer o reutilizar una instancia de MediaPlayer
title: Restablecer o reutilizar una instancia de MediaPlayer
uuid: 72cc4511-8ab0-44e5-b93c-b36f0321bba8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Restablecer, reutilizar o quitar una instancia de MediaPlayer {#reset-or-reuse-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

Cuando se restablece una instancia de MediaPlayer, se devuelve a su estado IDLE no inicializado tal como se define en MediaPlayerState.

Esta operación resulta útil en los siguientes casos:

* Desea reutilizar una instancia `MediaPlayer` pero necesita cargar un nuevo `MediaResource` (contenido de vídeo) y reemplazar la instancia anterior.

   Restablecer le permite reutilizar la instancia `MediaPlayer` sin necesidad de aprovechar la sobrecarga de liberar recursos, volver a crear `MediaPlayer` y reasignar recursos.

* Cuando `MediaPlayer` está en un estado ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado ERROR.

1. Llame a `reset` para devolver la instancia `MediaPlayer` a su estado no inicializado:

   ```java
   void reset() throws IllegalStateException; 
   ```

1. Utilice `MediaPlayer.replaceCurrentResource` para cargar otro `MediaResource`.

   >[!TIP]
   >
   >Para borrar un error, cargue el mismo `MediaResource`.

1. Cuando reciba la rellamada de evento `STATUS_CHANGED` con el estado PREPARADO, inicio la reproducción.

## Liberar una instancia y recursos de MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Debe liberar una instancia y recursos de MediaPlayer cuando ya no necesite MediaResource.

Cuando libera un objeto `MediaPlayer`, se desasignan los recursos de hardware subyacentes asociados a este objeto `MediaPlayer`.

A continuación se indican algunas razones para lanzar un MediaPlayer:

* La retención de recursos innecesarios puede afectar al rendimiento.
* Dejar un objeto `MediaPlayer` innecesario puede llevar a un consumo continuo de la batería para dispositivos móviles.
* Si no se admiten varias instancias del mismo códec de vídeo en un dispositivo, es posible que se produzca un error de reproducción en otras aplicaciones.

1. Libere el `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

Una vez liberada la instancia `MediaPlayer`, ya no podrá usarla. Si se llama a algún método de la interfaz `MediaPlayer` después de liberarlo, se genera un `IllegalStateException`.