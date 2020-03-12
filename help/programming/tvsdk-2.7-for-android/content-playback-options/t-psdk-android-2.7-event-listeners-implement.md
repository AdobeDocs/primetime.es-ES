---
description: Los controladores de eventos le permiten responder a eventos de TVSDK.
seo-description: Los controladores de eventos le permiten responder a eventos de TVSDK.
seo-title: Implementar escuchas de eventos y rellamadas
title: Implementar escuchas de eventos y rellamadas
uuid: bb1980f3-340b-4d36-ae7e-c9fc1d145233
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Implementar escuchas de eventos y rellamadas {#implement-event-listeners-and-callbacks}

Los controladores de eventos le permiten responder a eventos de TVSDK.

Cuando se produce un evento, el mecanismo de eventos de TVSDK llama al controlador de eventos registrado y le pasa la información del evento.

TVSDK define los oyentes como interfaces internas públicas dentro de la `MediaPlayer` interfaz.

La aplicación debe implementar detectores de eventos para cualquier evento TVSDK que afecte a la aplicación.

1. Determine qué eventos debe escuchar la aplicación.

   * Eventos requeridos: Escuche todos los eventos de reproducción.

      >[!IMPORTANT]
      >
      >Escuche el evento de cambio de estado, que se produce cuando el estado del reproductor cambia de formas que necesite saber. La información que proporciona incluye errores que pueden afectar a lo que el reproductor puede hacer a continuación.

   * Para otros eventos, según la aplicación, consulte events-summary.

1. Implemente y agregue un detector de eventos para cada evento.

   >[!NOTE]
   >
   >Para la mayoría de los eventos, TVSDK pasa argumentos a los oyentes de eventos. Estos valores proporcionan información sobre el evento que puede ayudarle a decidir qué hacer a continuación. La `MediaPlayerEvent` enumeración enumera todos los eventos que `MediaPlayer` se distribuyen. Para obtener más información, consulte events-summary .

   Por ejemplo, si `mPlayer` es una instancia de `MediaPlayer`, puede agregar y estructurar un detector de eventos:

   ```java
   mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() { 
       @Override 
       public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
           event.getMetadata(); 
           if (event.getMetadata() != null) {/* Do something */} 
           if (event.getStatus() == MediaPlayerStatus.IDLE) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.INITIALIZED) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.PREPARED) {/* Do something */} 
       } 
   }); 
   ```

## Orden de los eventos de reproducción {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK distribuye eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

Los siguientes ejemplos muestran el orden de algunos eventos que se producen durante la reproducción.

Cuando se carga correctamente un recurso de medios a través de `MediaPlayer.replaceCurrentResource`, el orden de los eventos es:

1. `MediaPlayerEvent.STATUS_CHANGED` con estado `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` con estado `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>Cargue el recurso de medios en el subproceso principal. Si carga un recurso de medios en un subproceso en segundo plano, esta operación o operaciones posteriores podrían generar un error, como `MediaPlayerException`y salir.

Al prepararse para la reproducción a través de `MediaPlayer.prepareToPlay`, el orden de los eventos es:

1. `MediaPlayerEvent.STATUS_CHANGED` con estado `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` si se insertaron publicidades.
1. `MediaPlayerEvent.STATUS_CHANGED` con estado `MediaPlayerStatus.PREPARED`

Para flujos en directo/lineal, durante la reproducción a medida que avanza la ventana de reproducción y se resuelven oportunidades adicionales, el orden de los eventos es:

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` si se insertaron publicidades

## Orden de los eventos publicitarios {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

Cuando la reproducción incluye publicidad, TVSDK distribuye eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos dentro de la secuencia esperada.

Al reproducir publicidades, el orden de los eventos es:

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

Los siguientes eventos se envían para cada publicidad dentro de la pausa publicitaria:

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

El siguiente ejemplo muestra una progresión típica de los eventos de reproducción de publicidad:

```
mediaPlayer.addEventListener(MediaPlayerEvent.AD_RESOLUTION_COMPLETE, new AdResolutionCompleteEventListener() { 
        @Override 
        public void onAdResolutionComplete() { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_START, new AdBreakStartedEventListener() { 
         @Override 
        public void onAdBreakStarted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_START, new AdStartedEventListener() { 
         @Override 
        public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_PROGRESS, new AdProgressEventListener() { 
         @Override 
         public void onAdProgress(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_COMPLETE, new AdCompletedEventListener() { 
         @Override 
         public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_COMPLETE, new AdBreakCompletedEventListener() { 
         @Override 
         public void onAdBreakCompleted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
Below event is for tracking ad clicks. 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_CLICK, new AdClickedEventListener() { 
         @Override 
         public void onAdClicked(AdClickEvent adClickEvent) { ... } 
    });
```

## Orden de los eventos de DRM {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM como, por ejemplo, cuando hay disponibles nuevos metadatos DRM. El reproductor puede implementar acciones en respuesta a estos eventos.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, escuche `MediaPlayerEvent.DRM_METADATA`. TVSDK distribuye eventos DRM adicionales a través de la `DRMManager` clase.

## Orden de los eventos de cargador {#section_5638F8EDACCE422A9425187484D39DCC}

TVSDK se distribuye `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` cuando se producen eventos de cargador.