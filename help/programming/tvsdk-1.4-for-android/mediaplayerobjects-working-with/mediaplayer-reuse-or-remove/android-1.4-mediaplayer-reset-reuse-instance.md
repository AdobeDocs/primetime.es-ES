---
description: Cuando se restablece una instancia de MediaPlayer, se devuelve a su estado IDLE no inicializado tal como se define en MediaPlayerState.
seo-description: Cuando se restablece una instancia de MediaPlayer, se devuelve a su estado IDLE no inicializado tal como se define en MediaPlayerState.
seo-title: Restablecer o reutilizar una instancia de MediaPlayer
title: Restablecer o reutilizar una instancia de MediaPlayer
uuid: 72cc4511-8ab0-44e5-b93c-b36f0321bba8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Restablecer, reutilizar o quitar una instancia de MediaPlayer {#reset-or-reuse-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

Cuando se restablece una instancia de MediaPlayer, se devuelve a su estado IDLE no inicializado tal como se define en MediaPlayerState.

Esta operación resulta útil en los siguientes casos:

* Desea reutilizar una `MediaPlayer` instancia, pero debe cargar un nuevo `MediaResource` (contenido de vídeo) y reemplazar la instancia anterior.

   Restablecer le permite reutilizar la `MediaPlayer` instancia sin la sobrecarga de liberar recursos, volver a crearlos `MediaPlayer`y reasignar recursos.

* Cuando `MediaPlayer` se encuentra en un estado ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado ERROR.

1. Llamada `reset` para devolver la `MediaPlayer` instancia a su estado no inicializado:

   ```java
   void reset() throws IllegalStateException; 
   ```

1. Utilícelo `MediaPlayer.replaceCurrentResource` para cargar otro `MediaResource`.

   >[!TIP]
   >
   >Para borrar un error, cargue lo mismo `MediaResource`.

1. Cuando reciba la rellamada del `STATUS_CHANGED` evento con el estado PREPARADO, inicie la reproducción.

## Liberar una instancia y recursos de MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Debe liberar una instancia y recursos de MediaPlayer cuando ya no necesite MediaResource.

Al soltar un `MediaPlayer` objeto, se desasignan los recursos de hardware subyacentes asociados a este `MediaPlayer` objeto.

A continuación se indican algunas razones para lanzar un MediaPlayer:

* La retención de recursos innecesarios puede afectar al rendimiento.
* Dejar un `MediaPlayer` objeto innecesario puede llevar a un consumo continuo de batería para dispositivos móviles.
* Si no se admiten varias instancias del mismo códec de vídeo en un dispositivo, es posible que se produzca un error de reproducción en otras aplicaciones.

1. Libere el `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

Una vez liberada la `MediaPlayer` instancia, ya no podrá utilizarla. Si se llama a algún método de la `MediaPlayer` interfaz después de liberarlo, se `IllegalStateException` genera un error.