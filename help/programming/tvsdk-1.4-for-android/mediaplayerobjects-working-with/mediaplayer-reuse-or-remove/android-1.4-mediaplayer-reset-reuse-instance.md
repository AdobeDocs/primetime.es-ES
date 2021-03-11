---
description: Cuando se restablece una instancia de MediaPlayer, se vuelve a su estado IDLE sin inicializar tal como se define en MediaPlayerState.
title: Restablecer o reutilizar una instancia de MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---


# Restablecer, reutilizar o quitar una instancia de MediaPlayer {#reset-or-reuse-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

Cuando se restablece una instancia de MediaPlayer, se vuelve a su estado IDLE sin inicializar tal como se define en MediaPlayerState.

Esta operación resulta útil en los siguientes casos:

* Desea reutilizar una instancia `MediaPlayer` pero debe cargar un nuevo `MediaResource` (contenido de vídeo) y reemplazar la instancia anterior.

   El restablecimiento le permite reutilizar la instancia `MediaPlayer` sin necesidad de liberar recursos, volver a crear `MediaPlayer` y reasignar recursos.

* Cuando el `MediaPlayer` está en estado ERROR y debe borrarse.

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

1. Cuando reciba la llamada de retorno de evento `STATUS_CHANGED` con el estado PREPARADO, inicie la reproducción.

## Liberar una instancia y recursos de MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Debe liberar una instancia y recursos de MediaPlayer cuando ya no necesite MediaResource.

Cuando libera un objeto `MediaPlayer`, se desasignan los recursos de hardware subyacentes asociados a este objeto `MediaPlayer`.

Estas son algunas razones para lanzar un MediaPlayer:

* Mantener recursos innecesarios puede afectar al rendimiento.
* Dejar un objeto `MediaPlayer` innecesario puede llevar a un consumo continuo de batería para dispositivos móviles.
* Si en un dispositivo no se admiten varias instancias del mismo códec de vídeo, puede ocurrir un error de reproducción en otras aplicaciones.

1. Suelte el `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

Una vez lanzada la instancia `MediaPlayer`, ya no puede usarla. Si se llama a algún método de la interfaz `MediaPlayer` después de su lanzamiento, se genera un `IllegalStateException`.