---
description: Puede especificar si desea permitir la reproducción antes de que todas las publicidades se carguen y se coloquen en la línea de tiempo. Al iniciar la reproducción de este modo, el visor obtiene un acceso más rápido al contenido principal. Esta función solo se aplica a DVR en directo y no funciona con, digamos, los activos de VOD.
seo-description: Puede especificar si desea permitir la reproducción antes de que todas las publicidades se carguen y se coloquen en la línea de tiempo. Al iniciar la reproducción de este modo, el visor obtiene un acceso más rápido al contenido principal. Esta función solo se aplica a DVR en directo y no funciona con, digamos, los activos de VOD.
seo-title: Habilitar la carga de publicidad diferida
title: Habilitar la carga de publicidad diferida
uuid: ac7c8801-7fa2-4f17-b79c-c603b3236948
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Habilitar la carga de publicidad diferida{#enable-lazy-ad-loading}

Puede especificar si desea permitir la reproducción antes de que todas las publicidades se carguen y se coloquen en la línea de tiempo. Al iniciar la reproducción de este modo, el visor obtiene un acceso más rápido al contenido principal. Esta función solo se aplica a DVR en directo y no funciona con, digamos, los activos de VOD.

1. Utilice la propiedad booleana `delayAdLoading` en `AdvertisingMetadata`.

   * Cuando es false, TVSDK espera hasta que todas las publicidades se resuelvan y se coloquen antes de pasar al estado PREPARADO. De forma predeterminada, es false.
   * Cuando el valor es true, TVSDK solo resuelve las publicidades iniciales y las transiciones al estado PREPARADO. Las demás publicidades se resuelven y se colocan durante la reproducción.

1. Para activar también la carga de anuncios retrasados con Adobe Primetime y la toma de decisiones, establezca este valor en `true` al crear `AuditudeSettings`.

   La `AuditudeSettings` clase hereda esta propiedad de `AdvertisingMetadata`, pero no hereda el valor actual.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. Para reflejar con precisión los anuncios como señales en una barra de desplazamiento, escuche los `TimelineEvent`. `TIMELINE_UPDATED` y vuelva a dibujar la barra de desplazamiento cada vez que reciba este evento.

   Cuando los flujos de VoD usan carga de publicidad retrasada, no todos los anuncios se colocan en la línea de tiempo cuando el reproductor entra en el estado PREPARADO, por lo que debe volver a dibujar explícitamente la barra de desplazamiento.

   TVSDK optimiza el envío de este evento para minimizar el número de veces que debe volver a dibujar la barra de desplazamiento; por lo tanto, el número de eventos de línea de tiempo no está relacionado con el número de pausas publicitarias que se deben colocar en la línea de tiempo. Por ejemplo: si tiene cinco pausas publicitarias, es posible que no reciba exactamente cinco eventos.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```

