---
description: Puede habilitar o deshabilitar la función de resolución de publicidad diferida mediante el mecanismo de carga de publicidad diferida existente (la resolución de publicidad diferida está deshabilitada de forma predeterminada).
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: Puede habilitar o deshabilitar la función de resolución de publicidad diferida mediante el mecanismo de carga de publicidad diferida existente (la resolución de publicidad diferida está deshabilitada de forma predeterminada).
seo-title: Habilitar la resolución diferida de publicidad
title: Habilitar la resolución diferida de publicidad
uuid: 91884eea-a622-4f5d-b6a8-36bb0050ba1d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Habilitar la resolución de publicidad diferida {#enable-lazy-ad-resolving}

Puede habilitar o deshabilitar la función de resolución de publicidad diferida mediante el mecanismo de carga de publicidad diferida existente (la resolución de publicidad diferida está deshabilitada de forma predeterminada).

Puede habilitar o deshabilitar la resolución de publicidad diferida llamando a [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con true o false.

* Utilice los métodos booleanos *hasDelayAdLoading* y *setDelayAdLoading* en AdvertisingMetadata para controlar la temporización de la resolución de publicidad y la colocación de las publicidades en la línea de tiempo:

   * Si *hasDelayAdLoading* devuelve false, TVSDK espera hasta que todas las publicidades se resuelvan y se coloquen antes de realizar la transición al estado PREPARADO.
   * Si *hasDelayAdLoading* devuelve true, TVSDK solo resuelve las publicidades y transiciones iniciales en el estado PREPARADO.

      * Las demás publicidades se resuelven y se colocan durante la reproducción.
   * Cuando *hasPreroll *o *hasLivePreroll* devuelve false, TVSDK supone que no hay anuncios previos y inicio la reproducción del contenido inmediatamente. Estos valores predeterminados están establecidos en true.


**API relevantes para la resolución de publicidad diferida:**

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

Cuando la resolución diferida de publicidad está habilitada para los flujos de VOD, todos los saltos de publicidad se colocan en la línea de tiempo; sin embargo, muchos de los saltos de publicidad aún no se resolverán. La aplicación puede determinar si desea o no dibujar estos marcadores seleccionando `TimelineMarker::getDuration()`. Si el valor es bueno a cero, las publicidades dentro de la pausa publicitaria se han resuelto.

TVSDK distribuye este evento cuando se ha resuelto una pausa publicitaria y también cuando el reproductor transición al estado PREPARADO.

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
