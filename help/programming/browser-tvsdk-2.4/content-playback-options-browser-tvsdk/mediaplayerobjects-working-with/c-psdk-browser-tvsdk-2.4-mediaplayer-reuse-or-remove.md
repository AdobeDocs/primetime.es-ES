---
description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
seo-description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
seo-title: Reutilización o eliminación de una instancia de MediaPlayer
title: Reutilización o eliminación de una instancia de MediaPlayer
uuid: 0b9a06b0-ece7-4e18-9221-a4528bcbc141
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Reutilizar o quitar una instancia de MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

## Restablecer o reutilizar una instancia de MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

Puede restablecer una instancia `MediaPlayer` para devolverla a su estado IDLE no inicializado, tal como se define en `MediaPlayerStatus`. También puede reemplazar el elemento de medios actual o establecer uno nuevo con un recurso de medios cargado previamente.

Esta operación resulta útil en los siguientes casos:

* Desea reutilizar una instancia `MediaPlayer` pero necesita cargar un nuevo `MediaResource` (contenido de vídeo) y reemplazar la instancia anterior.

   Restablecer le permite reutilizar la instancia `MediaPlayer` sin necesidad de aprovechar la sobrecarga de liberar recursos, volver a crear `MediaPlayer` y reasignar recursos. El método `replaceCurrentItem` realiza automáticamente estos pasos.

* Cuando `MediaPlayer` está en un estado ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado ERROR.

1. Llame a `MediaPlayer.reset()` para devolver la instancia `MediaPlayer` a su estado no inicializado:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Llame a `MediaPlayer.replaceCurrentItem()` para cargar otro `MediaResource`

   >[!TIP]
   >
   >Para borrar un error, cargue el mismo `MediaResource`.

1. Llame al método `prepareToPlay()`.

   >[!NOTE]
   >
   >Cuando recibe el evento `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con el estado PREPARADO, puede realizar el inicio de la reproducción.

## Liberar una instancia y recursos de MediaPlayer {#section_2D159975C82245098E7078FE0B1578CE}

Debe liberar una instancia `MediaPlayer` y recursos cuando ya no necesite MediaResource.

A continuación se indican algunas razones para lanzar un `MediaPlayer`:

* La retención de recursos innecesarios puede afectar al rendimiento.
* Dejar un objeto `MediaPlayer` innecesario puede llevar a un consumo continuo de la batería para dispositivos móviles.
* Si no se admiten varias instancias del mismo códec de vídeo en un dispositivo, es posible que se produzca un error de reproducción en otras aplicaciones.

* Libere el `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Una vez liberada la instancia `MediaPlayer`, ya no podrá usarla. Si se llama a algún método de la interfaz `MediaPlayer` después de liberarlo, se genera un `IllegalStateException`.

