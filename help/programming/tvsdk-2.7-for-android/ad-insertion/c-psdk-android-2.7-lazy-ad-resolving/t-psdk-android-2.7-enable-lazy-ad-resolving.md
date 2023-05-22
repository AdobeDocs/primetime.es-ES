---
description: Puede activar o desactivar la función de resolución de anuncios diferidos mediante el mecanismo de carga de anuncios diferidos existente (la resolución de anuncios diferidos está activada de forma predeterminada).
keywords: Diferido;Resolución de publicidad;Carga de publicidad;delayLoading
title: Habilitar la resolución de anuncios diferidos
exl-id: 4cd53ace-b0f5-4eef-93c3-644c2f48ce49
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Habilitar la resolución de anuncios diferidos {#enable-lazy-ad-resolving}

Puede activar o desactivar la función de resolución de anuncios diferidos mediante el mecanismo de carga de anuncios diferidos existente (la resolución de anuncios diferidos está activada de forma predeterminada).

Puede habilitar o deshabilitar la resolución de anuncios diferidos llamando a [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con `true` o `false`.

1. Utilice el valor booleano `hasDelayAdLoading` y `setDelayAdLoading` métodos en `AdvertisingMetadata` para controlar el tiempo de resolución de anuncios y la ubicación de los anuncios en la cronología:

   * If `hasDelayAdLoading` devuelve false, TVSDK espera hasta que todos los anuncios se resuelvan y se coloquen antes de pasar al estado PREPARED.
   * If `hasDelayAdLoading` devuelve true, TVSDK resuelve solo los anuncios iniciales y las transiciones al estado PREPARED. Los anuncios restantes se resuelven y se colocan durante la reproducción.
   * Cuándo `hasPreroll` o `hasLivePreroll` devuelve false, TVSDK supone que no hay ningún anuncio preroll e inicia la reproducción del contenido inmediatamente. El valor predeterminado es true.

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

1. Para reflejar los anuncios con precisión como indicaciones en una barra de desplazamiento, escuche la `TimelineEvent` y vuelva a dibujar la barra de desplazamiento cada vez que reciba este evento.

   Cuando la resolución de anuncios diferidos está habilitada para flujos de VOD, no todos los anuncios se colocan en la cronología cuando el reproductor entra en el estado PREPARADO, por lo que el reproductor debe volver a dibujar explícitamente la barra de desplazamiento.

   TVSDK optimiza el envío de este evento para minimizar el número de veces que debe volver a dibujar la barra de desplazamiento; por lo tanto, el número de eventos de cronología no está relacionado con el número de pausas publicitarias que se colocan en la cronología. Por ejemplo, si tiene cinco pausas publicitarias, es posible que no reciba exactamente cinco eventos.

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

>Para comprobar si la función de resolución de anuncios diferidos está habilitada o deshabilitada, llame a `AdvertisingMetadata.hasDelayAdLoading`. Un valor devuelto de `true` significa que la resolución de anuncios diferidos está habilitada; `false` significa que la función está deshabilitada.
