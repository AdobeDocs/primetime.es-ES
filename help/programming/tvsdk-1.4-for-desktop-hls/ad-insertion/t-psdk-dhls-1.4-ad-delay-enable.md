---
description: Puede especificar si desea permitir la reproducción antes de que todos los anuncios se carguen y se coloquen en la cronología. Iniciar la reproducción de esta manera permite que el usuario acceda más rápido al contenido principal. Esta función solo se aplica al DVR en directo y no funciona, por ejemplo, en los recursos de VOD.
title: Habilitar la carga diferida de anuncios
exl-id: 6b70a7ae-28ce-4a19-9560-26e937c721cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Habilitar la carga diferida de anuncios{#enable-lazy-ad-loading}

Puede especificar si desea permitir la reproducción antes de que todos los anuncios se carguen y se coloquen en la cronología. Iniciar la reproducción de esta manera permite que el usuario acceda más rápido al contenido principal. Esta función solo se aplica al DVR en directo y no funciona, por ejemplo, en los recursos de VOD.

1. Usar la propiedad booleana `delayAdLoading` in `AdvertisingMetadata`.

   * Cuando es false, TVSDK espera hasta que todos los anuncios se resuelvan y se coloquen antes de pasar al estado PREPARED. De forma predeterminada, es false.
   * Cuando es true, TVSDK resuelve solo los anuncios iniciales y las transiciones al estado PREPARED. Los anuncios restantes se resuelven y se colocan durante la reproducción.

1. Para activar también la carga de publicidad retrasada con Adobe Primetime ad Decisioning, establézcalo en `true` al crear `AuditudeSettings`.

   El `AuditudeSettings` La clase hereda esta propiedad de `AdvertisingMetadata`, pero no hereda el valor actual.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. Para reflejar los anuncios con precisión como indicaciones en una barra de desplazamiento, escuche la `TimelineEvent`. `TIMELINE_UPDATED` y vuelva a dibujar la barra de desplazamiento cada vez que reciba este evento.

   Cuando los flujos VoD utilizan la carga de anuncios retrasada, no todos los anuncios se colocan en la cronología cuando el reproductor entra en el estado PREPARADO, por lo que debe volver a dibujar explícitamente la barra de desplazamiento.

   TVSDK optimiza el envío de este evento para minimizar el número de veces que debe volver a dibujar la barra de desplazamiento; por lo tanto, el número de eventos de cronología no está relacionado con el número de pausas publicitarias que se colocan en la cronología. Por ejemplo, si tiene cinco pausas publicitarias, es posible que no reciba exactamente cinco eventos.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```
