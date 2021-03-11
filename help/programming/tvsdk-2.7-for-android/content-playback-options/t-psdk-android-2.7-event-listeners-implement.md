---
description: Los controladores de eventos permiten responder a los eventos de TVSDK.
title: Implementación de oyentes de eventos y llamadas de retorno
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Implementar oyentes de eventos y llamadas de retorno {#implement-event-listeners-and-callbacks}

Los controladores de eventos permiten responder a los eventos de TVSDK.

Cuando se produce un evento, el mecanismo de eventos de TVSDK llama al controlador de eventos registrado y le pasa la información del evento.

TVSDK define los oyentes como interfaces internas públicas dentro de la interfaz `MediaPlayer`.

La aplicación debe implementar detectores de eventos para cualquier evento TVSDK que afecte a la aplicación.

1. Determine qué eventos debe escuchar la aplicación.

   * Eventos necesarios: Escuche todos los eventos de reproducción.

      >[!IMPORTANT]
      >
      >Escuche el evento de cambio de estado, que se produce cuando el estado del reproductor cambia de formas que necesite saber. La información que proporciona incluye errores que podrían afectar a lo que el reproductor puede hacer a continuación.

   * Para otros eventos, según la aplicación, consulte resumen de eventos .

1. Implemente y agregue un detector de eventos para cada evento.

   >[!NOTE]
   >
   >Para la mayoría de los eventos, TVSDK pasa argumentos a los oyentes de eventos. Estos valores proporcionan información sobre el evento que puede ayudarle a decidir qué hacer a continuación. La enumeración `MediaPlayerEvent` enumera todos los eventos que `MediaPlayer` envía. Para obtener más información, consulte resumen de eventos .

   Por ejemplo, si `mPlayer` es una instancia de `MediaPlayer`, así es como puede agregar y estructurar un detector de eventos:

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

TVSDK envía eventos/notificaciones en secuencias esperadas generalmente. El reproductor puede implementar acciones basadas en eventos en la secuencia esperada.

Los siguientes ejemplos muestran el orden de algunos eventos que se producen durante la reproducción.

Cuando se carga correctamente un recurso de medios a través de `MediaPlayer.replaceCurrentResource`, el orden de los eventos es:

1. `MediaPlayerEvent.STATUS_CHANGED` con estado  `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` con estado  `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>Cargue el recurso de medios en el subproceso principal. Si carga un recurso de medios en un subproceso en segundo plano, esta operación u operaciones posteriores podrían generar un error, como `MediaPlayerException`, y salir.

Al prepararse para la reproducción mediante `MediaPlayer.prepareToPlay`, el orden de los eventos es:

1. `MediaPlayerEvent.STATUS_CHANGED` con estado  `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` si se insertaron anuncios.
1. `MediaPlayerEvent.STATUS_CHANGED` con estado  `MediaPlayerStatus.PREPARED`

Para emisiones en directo/lineales, durante la reproducción a medida que avanza la ventana de reproducción y se resuelven las oportunidades adicionales, el orden de los eventos es:

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` si se insertaron anuncios

## Orden de los eventos publicitarios {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

Cuando la reproducción incluye publicidad, TVSDK envía eventos/notificaciones en secuencias generalmente esperadas. El reproductor puede implementar acciones basadas en eventos dentro de la secuencia esperada.

Al reproducir anuncios, el orden de los eventos es:

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

Los siguientes eventos se envían para cada anuncio dentro de la pausa publicitaria:

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

TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM, como cuando nuevos metadatos DRM están disponibles. El reproductor puede implementar acciones en respuesta a estos eventos.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, escuche `MediaPlayerEvent.DRM_METADATA`. TVSDK distribuye eventos DRM adicionales a través de la clase `DRMManager`.

## Orden de los eventos del cargador {#section_5638F8EDACCE422A9425187484D39DCC}

TVSDK envía `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` cuando se producen eventos de cargador.