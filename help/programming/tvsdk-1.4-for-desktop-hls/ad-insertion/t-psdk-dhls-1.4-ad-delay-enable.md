---
description: Puede especificar si se permite la reproducción antes de que se carguen y se coloquen todos los anuncios en la cronología. El inicio de la reproducción de este modo permite al usuario acceder más rápido al contenido principal. Esta función solo es aplicable a DVR en directo y no funciona en, digamos, activos de VOD.
title: Habilitar la carga de publicidad diferida
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Habilitar carga de publicidad diferida{#enable-lazy-ad-loading}

Puede especificar si se permite la reproducción antes de que se carguen y se coloquen todos los anuncios en la cronología. El inicio de la reproducción de este modo permite al usuario acceder más rápido al contenido principal. Esta función solo es aplicable a DVR en directo y no funciona en, digamos, activos de VOD.

1. Utilice la propiedad booleana `delayAdLoading` en `AdvertisingMetadata`.

   * Cuando es false, TVSDK espera hasta que todos los anuncios se resuelvan y se coloquen antes de pasar al estado PREPARADO. Es false de forma predeterminada.
   * Cuando es verdadero, TVSDK resuelve solo los anuncios iniciales y las transiciones al estado PREPARADO. Los anuncios restantes se resuelven y se colocan durante la reproducción.

1. Para activar también la carga de anuncios retrasados con Adobe Primetime ad decisioning, configúrelo en `true` al crear `AuditudeSettings`.

   La clase `AuditudeSettings` hereda esta propiedad de `AdvertisingMetadata`, pero no hereda el valor actual.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. Para reflejar con precisión los anuncios como señales en una barra de desplazamiento, escuche el `TimelineEvent`. `TIMELINE_UPDATED` y vuelva a dibujar la barra de desplazamiento cada vez que reciba este evento.

   Cuando las emisiones de VoD utilizan la carga de anuncios retrasada, no todos los anuncios se colocan en la cronología cuando el reproductor entra en el estado PREPARADO, por lo que debe volver a dibujar explícitamente la barra de desplazamiento.

   TVSDK optimiza el envío de este evento para minimizar el número de veces que debe volver a dibujar la barra de desplazamiento; por lo tanto, el número de eventos de cronología no está relacionado con el número de pausas publicitarias que se deben colocar en la cronología. Por ejemplo, si tiene cinco pausas publicitarias, es posible que no reciba exactamente cinco eventos.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```

