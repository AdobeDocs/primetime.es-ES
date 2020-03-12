---
description: Puede habilitar o deshabilitar la función de resolución de publicidad diferida mediante el mecanismo de carga de publicidad diferida existente (la resolución de publicidad diferida está habilitada de forma predeterminada).
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: Puede habilitar o deshabilitar la función de resolución de publicidad diferida mediante el mecanismo de carga de publicidad diferida existente (la resolución de publicidad diferida está habilitada de forma predeterminada).
seo-title: Habilitar la resolución diferida de publicidad
title: Habilitar la resolución diferida de publicidad
uuid: a084ee0b-53af-4600-91f6-d30ccc89699d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Habilitar la resolución diferida de publicidad {#enable-lazy-ad-resolving}

Puede habilitar o deshabilitar la función de resolución de publicidad diferida mediante el mecanismo de carga de publicidad diferida existente (la resolución de publicidad diferida está habilitada de forma predeterminada).

Puede habilitar o deshabilitar la resolución de publicidad diferida llamando a [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con `true` o `false`.

1. Utilice los métodos booleanos `hasDelayAdLoading` y `setDelayAdLoading` en `AdvertisingMetadata` para controlar la temporización de la resolución de publicidad y la colocación de las publicidades en la línea de tiempo:

   * Si `hasDelayAdLoading` devuelve false, TVSDK espera hasta que todas las publicidades se resuelvan y se coloquen antes de realizar la transición al estado PREPARADO.
   * Si `hasDelayAdLoading` devuelve true, TVSDK solo resuelve las publicidades y transiciones iniciales al estado PREPARADO. Las demás publicidades se resuelven y se colocan durante la reproducción.
   * Cuando `hasPreroll` o `hasLivePreroll` devuelve false, TVSDK supone que no hay anuncios previos e inicia la reproducción del contenido inmediatamente. De forma predeterminada, se establece en true.

      API relevantes para la resolución de publicidad diferida:

      ```
      Class: 
         com.adobe.mediacore.metadata.AdvertisingMetadata 
      
      Methods: 
      […] 
          public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
          public final void setDelayAdLoading()    // Enable or disable Lazy Ad Resolving 
          public final boolean hasPreroll()        // Check for existence of pre-roll ads 
          public final void setPreroll()           // Set pre-roll true or false 
          public final boolean hasLivePreroll()    // Check for live pre-roll ads 
          public final void setLivePreroll()       // Set live pre-roll true or false 
      […]
      ```

1. Para reflejar con precisión los anuncios como señales en una barra de desplazamiento, escuche el `TimelineEvent` evento y vuelva a dibujar la barra de desplazamiento cada vez que reciba este evento.

   Cuando la resolución diferida de publicidad está habilitada para los flujos de VOD, no todos los anuncios se colocan en la línea de tiempo cuando el reproductor entra en el estado PREPARADO, por lo que el reproductor debe volver a dibujar explícitamente la barra de desplazamiento.

   TVSDK optimiza el envío de este evento para minimizar el número de veces que debe volver a dibujar la barra de desplazamiento; por lo tanto, el número de eventos de línea de tiempo no está relacionado con el número de pausas publicitarias que se deben colocar en la línea de tiempo. Por ejemplo: si tiene cinco pausas publicitarias, es posible que no reciba exactamente cinco eventos.

   ```java
   mediaPlayer.addEventListener 
       (MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
   /** 
    * ... 
    */ 
   public void onTimelineUpdated(TimelineEvent event) { 
   
       for (PlaybackManagerEventListener listener : eventListeners) { 
           listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
       } 
   } 
   ```

>Para verificar si la función de resolución de publicidad diferida está habilitada o deshabilitada, llame a `AdvertisingMetadata.hasDelayAdLoading`. Un valor devuelto de `true` significa que la resolución de publicidad diferida está habilitada; `false` significa que la función está deshabilitada.

