---
description: Puede habilitar o deshabilitar la función de resolución de anuncios diferidos mediante el mecanismo de carga de anuncios diferidos existente (la resolución de anuncios diferidos está habilitada de forma predeterminada).
keywords: Aceite;resolución de publicidad;carga de publicidad;delayLoading
title: Habilitar la resolución de anuncios diferidos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# Habilitar la resolución de anuncios diferidos {#enable-lazy-ad-resolving}

Puede habilitar o deshabilitar la función de resolución de anuncios diferidos mediante el mecanismo de carga de anuncios diferidos existente (la resolución de anuncios diferidos está habilitada de forma predeterminada).

Puede habilitar o deshabilitar la resolución de publicidad diferida llamando a [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con `true` o `false`.

1. Utilice los métodos booleanos `hasDelayAdLoading` y `setDelayAdLoading` de `AdvertisingMetadata` para controlar la temporización de la resolución de la publicidad y la colocación de la publicidad en la cronología:

   * Si `hasDelayAdLoading` devuelve el valor false, TVSDK espera hasta que se resuelvan y se coloquen todos los anuncios antes de pasar al estado PREPARADO.
   * Si `hasDelayAdLoading` devuelve el valor &quot;True&quot;, TVSDK solo resuelve los anuncios iniciales y las transiciones al estado PREPARADO. Los anuncios restantes se resuelven y se colocan durante la reproducción.
   * Cuando `hasPreroll` o `hasLivePreroll` devuelven false, TVSDK supone que no hay anuncios previos a la publicación e inicia la reproducción del contenido inmediatamente. Estos valores predeterminados son true.

      API relevantes para la resolución de anuncios diferidos:

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

1. Para reflejar con precisión los anuncios como señales en una barra de desplazamiento, escuche el evento `TimelineEvent` y vuelva a dibujar la barra de desplazamiento cada vez que reciba este evento.

   Cuando la resolución de publicidad diferida está habilitada para las emisiones de VOD, no todos los anuncios se colocan en la cronología cuando el reproductor entra en el estado PREPARADO, por lo que el reproductor debe volver a dibujar explícitamente la barra de desplazamiento.

   TVSDK optimiza el envío de este evento para minimizar el número de veces que debe volver a dibujar la barra de desplazamiento; por lo tanto, el número de eventos de cronología no está relacionado con el número de pausas publicitarias que se deben colocar en la cronología. Por ejemplo, si tiene cinco pausas publicitarias, es posible que no reciba exactamente cinco eventos.

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

>Para verificar si la función de resolución de anuncios diferidos está habilitada o deshabilitada, llame a `AdvertisingMetadata.hasDelayAdLoading`. Un valor devuelto de `true` significa que la resolución de publicidad diferida está habilitada; `false` significa que la función está deshabilitada.

