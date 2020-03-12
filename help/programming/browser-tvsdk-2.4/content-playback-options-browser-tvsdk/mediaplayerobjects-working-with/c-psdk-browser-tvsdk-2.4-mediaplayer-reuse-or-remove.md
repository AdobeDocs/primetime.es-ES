---
description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
seo-description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
seo-title: Reutilización o eliminación de una instancia de MediaPlayer
title: Reutilización o eliminación de una instancia de MediaPlayer
uuid: 0b9a06b0-ece7-4e18-9221-a4528bcbc141
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Reutilización o eliminación de una instancia de MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

## Restablecer o reutilizar una instancia de MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

Puede restablecer una `MediaPlayer` instancia para devolverla a su estado IDLE no inicializado, tal como se define en `MediaPlayerStatus`. También puede reemplazar el elemento de medios actual o establecer uno nuevo con un recurso de medios cargado previamente.

Esta operación resulta útil en los siguientes casos:

* Desea reutilizar una `MediaPlayer` instancia, pero debe cargar un nuevo `MediaResource` (contenido de vídeo) y reemplazar la instancia anterior.

   Restablecer le permite reutilizar la `MediaPlayer` instancia sin la sobrecarga de liberar recursos, volver a crearlos `MediaPlayer`y reasignar recursos. El `replaceCurrentItem` método realiza automáticamente estos pasos.

* Cuando `MediaPlayer` se encuentra en un estado ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado ERROR.

1. Llamada `MediaPlayer.reset()` para devolver la `MediaPlayer` instancia a su estado no inicializado:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Llamar `MediaPlayer.replaceCurrentItem()` para cargar otro `MediaResource`

   >[!TIP]
   >
   >Para borrar un error, cargue lo mismo `MediaResource`.

1. Llame al `prepareToPlay()` método.

   >[!NOTE]
   >
   >Cuando recibe el `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` evento con el estado PREPARADO, puede iniciar la reproducción.

## Liberar una instancia y recursos de MediaPlayer {#section_2D159975C82245098E7078FE0B1578CE}

Debe liberar una `MediaPlayer` instancia y recursos cuando ya no necesite MediaResource.

A continuación se indican algunas razones para publicar un `MediaPlayer`:

* La retención de recursos innecesarios puede afectar al rendimiento.
* Dejar un `MediaPlayer` objeto innecesario puede llevar a un consumo continuo de batería para dispositivos móviles.
* Si no se admiten varias instancias del mismo códec de vídeo en un dispositivo, es posible que se produzca un error de reproducción en otras aplicaciones.

* Libere el `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Una vez liberada la `MediaPlayer` instancia, ya no podrá utilizarla. Si se llama a algún método de la `MediaPlayer` interfaz después de liberarlo, se `IllegalStateException` genera un error.

