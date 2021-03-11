---
description: Cuando los usuarios avancen o rebobinen rápidamente a través de los medios, se encuentran en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción engañosa, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
title: Implemente hacia adelante y rebobine rápidamente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Información general {#implement-fast-forward-and-rewind-overview}

Cuando los usuarios avancen o rebobinen rápidamente a través de los medios, se encuentran en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción engañosa, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.

Para cambiar la velocidad, debe establecer un valor.

1. Pase del modo de reproducción normal (1x) al modo de reproducción de trucos ajustando la velocidad en `MediaPlayer` a un valor permitido.

   * La clase `MediaPlayerItem` define las tasas de reproducción permitidas.
   * TVSDK selecciona la tasa permitida más cercana si no se permite la velocidad especificada.

   En este ejemplo se establece la velocidad de reproducción interna del reproductor en la velocidad solicitada.

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

1. Si lo desea, puede escuchar eventos de cambio de tasa, que le permiten saber cuándo solicitó un cambio de tasa y cuándo se produjo realmente un cambio de tasa.

       TVSDK distribuye los siguientes eventos relacionados con la reproducción trucada:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` cuando el  `rate` valor cambia a otro valor.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` cuando la reproducción se reanuda a la velocidad seleccionada.

      TVSDK envía ambos eventos cuando el reproductor vuelve del modo de reproducción trucada al modo de reproducción normal.

