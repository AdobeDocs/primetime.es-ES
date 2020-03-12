---
description: Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, establezca la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
seo-description: Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, establezca la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
seo-title: Implemente un avance rápido y rebobine
title: Implemente un avance rápido y rebobine
uuid: 070a3331-43a3-4517-9cd9-06d817ffcfbd
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Información general {#implement-fast-forward-and-rewind-overview}

Cuando los usuarios avanzan rápidamente o rebobinan rápidamente a través de los medios, están en el modo de reproducción mediante trucos. Para entrar en el modo de reproducción con trucos, establezca la velocidad de reproducción de MediaPlayer en un valor distinto de 1.

Para cambiar la velocidad, debe establecer un valor.

1. Pasar del modo de reproducción normal (1x) al modo de reproducción de trucos estableciendo la velocidad en el `MediaPlayer` a un valor permitido.

       Recuerde la siguiente información:
   
   * La `MediaPlayerItem` clase define las tasas de reproducción permitidas.
   * TVSDK selecciona la velocidad permitida más cercana si no se permite la velocidad especificada.

      El ejemplo siguiente establece la velocidad de reproducción interna del reproductor en la velocidad solicitada:

      ```
      import com.adobe.mediacore.MediaPlayer; 
      import com.adobe.mediacore.MediaPlayerItem; 
      import com.adobe.mediacore.MediaPlayerException; 
      import java.util.List; 
      import java.lang.Float; 
      
      private boolean setPlaybackRate(MediaPlayer player, float rate)  
        throws MediaPlayerException { 
          // Get list of playback rates that the media player supports 
          MediaPlayerItem item = player.getCurrentItem(); 
          if (item == null) return false; 
          List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
      
          // Return false if requested rate is not supported 
          if (availableRates.indexOf(rate) == -1) return false; 
      
          // Otherwise set the playback rate to the requested rate  
          // (this can throw MediaPlayerException) 
          player.setRate(rate); 
          return true; 
      }
      ```

1. De forma opcional, puede escuchar los eventos de cambio de tasa, que le avisan cuando solicita un cambio de tasa y cuando se produce el cambio de tasa.

       TVSDK distribuye los siguientes eventos relacionados con la reproducción mediante trucos:
   
   * `MediaPlayerEvent.RATE_SELECTED`, cuando el `rate` valor cambia a otro valor.

   * `MediaPlayerEvent.RATE_PLAYING`, cuando la reproducción se reanuda a la velocidad seleccionada.

      TVSDK distribuye estos eventos cuando el reproductor regresa del modo de reproducción ficticia al modo de reproducción normal.

