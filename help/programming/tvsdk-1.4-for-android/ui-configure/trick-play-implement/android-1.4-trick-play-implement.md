---
description: Cuando los usuarios avanzan o rebobinan rápidamente a través de los medios, se encuentran en el modo de reproducción con trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.
title: Implementar avance rápido y rebobinado
exl-id: 58ed9a96-9617-4364-81d4-b404b23cf265
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Información general {#implement-fast-forward-and-rewind-overview}

Cuando los usuarios avanzan o rebobinan rápidamente a través de los medios, se encuentran en el modo de reproducción con trucos. Para entrar en el modo de reproducción con trucos, debe establecer la velocidad de reproducción de MediaPlayer en un valor distinto de 1.

Para cambiar la velocidad, debe establecer un valor.

1. Cambie del modo de reproducción normal (1x) al modo de reproducción con trucos ajustando la velocidad en el `MediaPlayer` a un valor permitido.

   * El `MediaPlayerItem` define las velocidades de reproducción permitidas.
   * TVSDK selecciona la tasa permitida más cercana si la tasa especificada no está permitida.

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

1. Si lo desea, puede escuchar eventos de cambio de tarifa, que le permiten saber cuándo solicitó un cambio de tarifa y cuándo se produce realmente un cambio de tarifa.

       TVSDK envía los siguientes eventos relacionados con el juego de trucos:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` cuando la variable `rate` El valor cambia a un valor diferente.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` cuando la reproducción se reanuda a la velocidad seleccionada.

      TVSDK envía ambos eventos cuando el reproductor vuelve del modo de truco al modo de reproducción normal.
