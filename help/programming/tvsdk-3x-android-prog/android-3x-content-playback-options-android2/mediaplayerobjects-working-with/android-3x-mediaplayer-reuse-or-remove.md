---
description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
title: Reutilizar o quitar una instancia de MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# Reutilizar o quitar una instancia de MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

## Restablecer o reutilizar una instancia de MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Cuando se restablece una instancia `MediaPlayer`, se vuelve a su estado IDLE no inicializado tal como se define en `MediaPlayerStatus`.

Esta operación resulta útil en los siguientes casos:

* Desea reutilizar una instancia `MediaPlayer` pero debe cargar un nuevo `MediaResource` (contenido de vídeo) y reemplazar la instancia anterior.

   El restablecimiento le permite reutilizar la instancia `MediaPlayer` sin necesidad de liberar recursos, volver a crear `MediaPlayer` y reasignar recursos.

* Cuando el `MediaPlayer` está en estado ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado de ERROR.

   1. Llame a `reset` para devolver la instancia `MediaPlayer` a su estado no inicializado:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Utilice `MediaPlayer.replaceCurrentResource()` para cargar otro `MediaResource`.

      >[!NOTE]
      >
      >Para borrar un error, cargue el mismo `MediaResource`.

   1. Cuando reciba la llamada de retorno de evento `STATUS_CHANGED` con el estado `PREPARED`, inicie la reproducción.

## Liberar una instancia y recursos de MediaPlayer {#section_13A0914AFF784943ABC343F7EB249C4E}

Debe liberar una instancia y recursos `MediaPlayer` cuando ya no necesite el `MediaResource`.

Cuando libera un objeto `MediaPlayer`, se desasignan los recursos de hardware subyacentes asociados a este objeto `MediaPlayer`.

Estas son algunas razones para publicar un `MediaPlayer`:

* Mantener recursos innecesarios puede afectar al rendimiento.
* Dejar un objeto `MediaPlayer` innecesario creado como instancia puede llevar a un consumo continuo de batería para dispositivos móviles.
* Si hay varias instancias
Como el mismo códec de vídeo no se admite en un dispositivo, puede producirse un error de reproducción en otras aplicaciones.

* Suelte el `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Una vez lanzada la instancia `MediaPlayer`, ya no puede usarla. Si se llama a algún método de la interfaz `MediaPlayer` después de su lanzamiento, se genera un `MediaPlayerException`.