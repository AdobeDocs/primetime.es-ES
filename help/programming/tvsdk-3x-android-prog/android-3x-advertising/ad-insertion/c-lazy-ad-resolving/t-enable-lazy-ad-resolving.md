---
description: Puede habilitar o deshabilitar la función de resolución de publicidad diferida mediante el mecanismo de carga de publicidad diferida existente (la resolución de publicidad diferida está deshabilitada de forma predeterminada).
keywords: Aceite;resolución de publicidad;carga de publicidad;delayLoading
title: Habilitar la resolución de anuncios diferidos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# Habilitar la resolución de anuncios diferidos {#enable-lazy-ad-resolving}

Puede habilitar o deshabilitar la función de resolución de publicidad diferida mediante el mecanismo de carga de publicidad diferida existente (la resolución de publicidad diferida está deshabilitada de forma predeterminada).

Puede habilitar o deshabilitar la resolución de publicidad diferida llamando a [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con true o false.

* Utilice los métodos booleanos *hasDelayAdLoading* y *setDelayAdLoading* en AdvertisingMetadata para controlar la temporización de la resolución de la publicidad y la colocación de la publicidad en la cronología:

   * Si *hasDelayAdLoading* devuelve el valor false, TVSDK espera hasta que todos los anuncios se resuelvan y se coloquen antes de pasar al estado PREPARADO.
   * Si *hasDelayAdLoading* devuelve el valor &quot;True&quot;, TVSDK solo resuelve los anuncios iniciales y las transiciones al estado PREPARADO.

      * Los anuncios restantes se resuelven y se colocan durante la reproducción.
   * Cuando *hasPreroll *o *hasLivePreroll* devuelven false, TVSDK supone que no hay anuncios previos a la publicación e inicia la reproducción del contenido inmediatamente. Se establecen de forma predeterminada como verdadero.


**API relevantes para la resolución de anuncios diferidos:**

```
Class:    com.adobe.mediacore.metadata.AdvertisingMetadata 
Methods: 
    public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
    public final void setDelayAdLoading() // Enable or disable Lazy Ad Resolving 
    public final void setDelayAdLoadingTolerance() // Sets the Lazy Ad Resolving Tolerance level.  This value is added to the BufferControlParameters::playBufferTime and the content's EXT-X-TARGETDURATION to determine when ad breaks should resolve 
    public final double getDelayAdLoadingTolerance() // Gets the Lazy Ad Resolving Tolerance level 
    public final boolean hasPreroll() // Check for existence of pre-roll ads 
    public final void setPreroll() // Set pre-roll true or false 
    public final boolean hasLivePreroll() // Check for live pre-roll ads 
    public final void setLivePreroll() // Set live pre-roll true or false

Class:     com.adobe.mediacore.timeline.TimelineMarker 
Methods: 
    public double getDuration() // Returns the current duration of the TimelineMarker.  This will be zero if the ad break has not yet resolved. 
    public Placement.Type getPlacementType() // Returns whether
```

Para reflejar con precisión los anuncios como señales en una barra de desplazamiento, escuche el evento `TimelineEvent`y vuelva a dibujar la barra de desplazamiento cada vez que reciba este evento.

Cuando la resolución de publicidad diferida está habilitada para las emisiones de VOD, todas las pausas publicitarias se colocan en la cronología, sin embargo, muchas de las pausas publicitarias aún no se resolverán. La aplicación puede determinar si desea dibujar o no estos marcadores marcando el `TimelineMarker::getDuration()`. Si el valor es bueno a cero, se han resuelto los anuncios dentro de la pausa publicitaria.

TVSDK envía este evento cuando se ha resuelto una pausa publicitaria y también cuando el reproductor pasa al estado PREPARADO.

```
mediaPlayer.addEventListener(MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
/** 
* ... 
*/ 
public void onTimelineUpdated(TimelineEvent event) { 
for (PlaybackManagerEventListener listener : eventListeners) { 
  listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
}
```
