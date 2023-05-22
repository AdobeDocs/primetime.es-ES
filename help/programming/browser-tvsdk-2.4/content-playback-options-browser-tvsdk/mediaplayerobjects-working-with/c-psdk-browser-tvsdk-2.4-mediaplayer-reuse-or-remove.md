---
description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
title: Reutilización o eliminación de una instancia de MediaPlayer
exl-id: 2403e6dd-74c4-43fb-913a-d04e61041628
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Reutilización o eliminación de una instancia de MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

## Restablecer o reutilizar una instancia de MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

Puede restablecer un `MediaPlayer` para devolverla a su estado IDLE sin inicializar, tal como se define en `MediaPlayerStatus`. También puede reemplazar el elemento de medios actual o establecer uno nuevo mediante un recurso de medios cargado anteriormente.

Esta operación resulta útil en los siguientes casos:

* Desea volver a utilizar un `MediaPlayer` instancia, pero debe cargar una nueva `MediaResource` (contenido de vídeo) y reemplace la instancia anterior.

   El restablecimiento le permite reutilizar el `MediaPlayer` instancia sin los gastos generales de liberación de recursos, recreando la `MediaPlayer`y la reasignación de recursos. El `replaceCurrentItem` El método de realiza automáticamente estos pasos por usted.

* Si la variable `MediaPlayer` está en estado ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado ERROR.

1. Llamada `MediaPlayer.reset()` para devolver el `MediaPlayer` a su estado sin inicializar:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Llamada `MediaPlayer.replaceCurrentItem()` para cargar otro `MediaResource`

   >[!TIP]
   >
   >Para borrar un error, cargue el mismo `MediaResource`.

1. Llame a `prepareToPlay()` método.

   >[!NOTE]
   >
   >Cuando reciba la `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con el estado PREPARADO, puede iniciar la reproducción.

## Lanzamiento de una instancia de MediaPlayer y recursos {#section_2D159975C82245098E7078FE0B1578CE}

Debe publicar un `MediaPlayer` y recursos cuando ya no necesite el MediaResource.

Estas son algunas razones para publicar un `MediaPlayer`:

* Mantener recursos innecesarios puede afectar al rendimiento.
* Dejando un elemento innecesario `MediaPlayer` Este objeto puede consumir continuamente baterías para dispositivos móviles.
* Si no se admiten varias instancias del mismo códec de vídeo en un dispositivo, puede producirse un error de reproducción en otras aplicaciones.

* Suelte el `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Después del `MediaPlayer` Una vez liberada, ya no puede utilizarla. Si hay algún método del `MediaPlayer` se llama a la interfaz de después de su lanzamiento, y `IllegalStateException` se ha lanzado.
