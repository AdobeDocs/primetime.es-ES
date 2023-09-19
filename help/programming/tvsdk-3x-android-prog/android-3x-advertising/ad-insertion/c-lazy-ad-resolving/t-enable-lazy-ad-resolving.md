---
description: Puede activar o desactivar la función de resolución de anuncios diferidos mediante el mecanismo de carga de anuncios diferidos existente (la resolución de anuncios diferidos está desactivada de forma predeterminada).
keywords: Diferido;Resolución de publicidad;Carga de publicidad;delayLoading
title: Habilitar la resolución de anuncios diferidos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Habilitar la resolución de anuncios diferidos {#enable-lazy-ad-resolving}

Puede activar o desactivar la función de resolución de anuncios diferidos mediante el mecanismo de carga de anuncios diferidos existente (la resolución de anuncios diferidos está desactivada de forma predeterminada).

Puede habilitar o deshabilitar la resolución de anuncios diferidos llamando a [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con true o false.

* Utilice el valor booleano *hasDelayAdLoading* y *setDelayAdLoading* Métodos de Advertising Metadata para controlar el tiempo de resolución de anuncios y la ubicación de los anuncios en la cronología:

   * If *hasDelayAdLoading* devuelve false, TVSDK espera hasta que todos los anuncios se resuelvan y se coloquen antes de pasar al estado PREPARED.
   * If *hasDelayAdLoading* devuelve true, TVSDK resuelve solo los anuncios iniciales y las transiciones al estado PREPARED.

      * Los anuncios restantes se resuelven y se colocan durante la reproducción.

   * Cuando *hasPreroll *o *hasLivePreroll* devuelve false, TVSDK supone que no hay ningún anuncio preroll e inicia la reproducción del contenido inmediatamente. Se establecen en true de forma predeterminada.

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

Para reflejar los anuncios con precisión como indicaciones en una barra de desplazamiento, escuche la `TimelineEvent`y vuelva a dibujar la barra de desplazamiento cada vez que reciba este evento.

Cuando la resolución diferida de anuncios está habilitada para emisiones de VOD, todas las pausas publicitarias se colocan en la cronología; sin embargo, muchas de las pausas publicitarias no se resolverán aún. La aplicación puede determinar si se deben dibujar o no estos marcadores marcando la `TimelineMarker::getDuration()`. Si el valor es mayor que cero, se han resuelto los anuncios de la pausa publicitaria.

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
