---
description: Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
seo-description: Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
seo-title: Implemente un avance rápido y rebobine
title: Implemente un avance rápido y rebobine
uuid: 2e5d0fd0-0290-4f08-b9c6-c8ecde26abb8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Información general {#implement-fast-forward-and-rewind-overview}

Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.

Para cambiar la velocidad, debe establecer un valor.

1. Pasar del modo de reproducción normal (1x) al modo de reproducción de trucos estableciendo la velocidad en `MediaPlayer` a un valor permitido.

   * La clase `MediaPlayerItem` define las tasas de reproducción permitidas.
   * TVSDK selecciona la velocidad permitida más cercana si no se permite la velocidad especificada.

   Este ejemplo establece la velocidad de reproducción interna del reproductor en la velocidad solicitada.

   ```java
   import com.adobe.mediacore.MediaPlayer; 
   import com.adobe.mediacore.MediaPlayerItem; 
   import com.adobe.mediacore.MediaPlayerException; 
   import java.util.List; 
   import java.lang.Float; 
   
   private boolean setPlaybackRate(MediaPlayer player, float rate) throws MediaPlayerException  
   { 
       //Get list of playback rates that the media player supports 
       MediaPlayerItem item = player.getCurrentItem(); 
       if(item == null) return false; 
       List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
   
       //Return false if requested rate is not supported 
       if(availableRates.indexOf(rate) == -1) return false; 
   
       //Otherwise set the playback rate to the requested rate  
       //(this can throw MediaPlayerException) 
       player.setRate(rate); 
       return true; 
   }
   ```

1. De forma opcional, puede escuchar eventos de cambio de tasa, que le informarán cuando solicitó un cambio de tasa y cuando realmente se produce un cambio de tasa.

       TVSDK distribuye los siguientes eventos relacionados con la reproducción mediante trucos:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` cuando el  `rate` valor cambia a otro valor.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` cuando la reproducción se reanuda a la velocidad seleccionada.

      TVSDK distribuye ambos eventos cuando el reproductor regresa del modo de reproducción mediante trucos al modo de reproducción normal.

