---
description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
seo-description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
seo-title: Reutilización o eliminación de una instancia de MediaPlayer
title: Reutilización o eliminación de una instancia de MediaPlayer
uuid: 74a46689-1708-4d26-9a4e-a4cdb0e55451
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Reutilización o eliminación de una instancia de MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

## Restablecer o reutilizar una instancia de MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Cuando se restablece una `MediaPlayer` instancia, se devuelve a su estado IDLE no inicializado, tal como se define en `MediaPlayerStatus`.

Esta operación resulta útil en los siguientes casos:

* Desea reutilizar una `MediaPlayer` instancia, pero debe cargar un nuevo `MediaResource` (contenido de vídeo) y reemplazar la instancia anterior.

   Restablecer le permite reutilizar la `MediaPlayer` instancia sin la sobrecarga de liberar recursos, volver a crearlos `MediaPlayer`y reasignar recursos.

* Cuando `MediaPlayer` se encuentra en el estado ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado ERROR.

   1. Llamar `reset` para devolver la `MediaPlayer` instancia a su estado no inicializado:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Utilícelo `MediaPlayer.replaceCurrentResource()` para cargar otro `MediaResource`.

      >[!NOTE]
      >
      >Para borrar un error, cargue lo mismo `MediaResource`.

   1. Cuando reciba la llamada de retorno del `STATUS_CHANGED` evento con `PREPARED` estado, inicie la reproducción.

## Liberar una instancia y recursos de MediaPlayer {#section_13A0914AFF784943ABC343F7EB249C4E}

Debe liberar una `MediaPlayer` instancia y recursos cuando ya no necesite el `MediaResource`.

Al soltar un `MediaPlayer` objeto, se desasignan los recursos de hardware subyacentes asociados a este `MediaPlayer` objeto.

A continuación se indican algunas razones para publicar un `MediaPlayer`:

* La retención de recursos innecesarios puede afectar al rendimiento.
* Si se deja una instancia de un `MediaPlayer` objeto innecesaria, se puede producir un consumo continuo de la batería para dispositivos móviles.
* Si no se admiten varias instancias del mismo códec de vídeo en un dispositivo, es posible que se produzca un error de reproducción en otras aplicaciones.

* Libere el `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Una vez liberada la `MediaPlayer` instancia, ya no podrá utilizarla. Si se llama a algún método de la `MediaPlayer` interfaz después de liberarlo, se `MediaPlayerException` genera un error.