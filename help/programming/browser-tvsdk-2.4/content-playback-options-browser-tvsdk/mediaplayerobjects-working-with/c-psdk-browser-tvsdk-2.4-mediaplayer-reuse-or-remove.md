---
description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
title: Reutilizar o quitar una instancia de MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Reutilizar o quitar una instancia de MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

## Restablecer o reutilizar una instancia de MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

Puede restablecer una instancia `MediaPlayer` para devolverla a su estado IDLE no inicializado definido en `MediaPlayerStatus`. También puede reemplazar el elemento de medios actual o establecer uno nuevo mediante un recurso de medios cargado previamente.

Esta operación resulta útil en los siguientes casos:

* Desea reutilizar una instancia `MediaPlayer` pero debe cargar un nuevo `MediaResource` (contenido de vídeo) y reemplazar la instancia anterior.

   El restablecimiento le permite reutilizar la instancia `MediaPlayer` sin necesidad de liberar recursos, volver a crear `MediaPlayer` y reasignar recursos. El método `replaceCurrentItem` realiza automáticamente estos pasos.

* Cuando el `MediaPlayer` está en estado ERROR y debe borrarse.

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

1. Llame al método `prepareToPlay()` .

   >[!NOTE]
   >
   >Cuando reciba el evento `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con el estado PREPARADO, puede iniciar la reproducción.

## Liberar una instancia y recursos de MediaPlayer {#section_2D159975C82245098E7078FE0B1578CE}

Debe liberar una instancia y recursos `MediaPlayer` cuando ya no necesite MediaResource.

Estas son algunas razones para publicar un `MediaPlayer`:

* Mantener recursos innecesarios puede afectar al rendimiento.
* Dejar un objeto `MediaPlayer` innecesario puede llevar a un consumo continuo de batería para dispositivos móviles.
* Si en un dispositivo no se admiten varias instancias del mismo códec de vídeo, puede ocurrir un error de reproducción en otras aplicaciones.

* Suelte el `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Una vez lanzada la instancia `MediaPlayer`, ya no puede usarla. Si se llama a algún método de la interfaz `MediaPlayer` después de su lanzamiento, se genera un `IllegalStateException`.

