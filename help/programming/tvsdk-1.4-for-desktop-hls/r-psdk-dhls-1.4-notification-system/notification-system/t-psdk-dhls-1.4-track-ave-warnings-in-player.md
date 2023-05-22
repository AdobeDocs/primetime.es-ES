---
description: Con NotificationEvent, puede realizar un seguimiento de las advertencias que se transmiten desde el motor de vídeo de Adobe (AVE).
title: Seguimiento de advertencias de AVE en el reproductor
exl-id: 49118d7f-ed79-4d22-ba91-8929f97c7256
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Seguimiento de advertencias de AVE en el reproductor{#track-ave-warnings-in-your-player}

Con NotificationEvent, puede realizar un seguimiento de las advertencias que se transmiten desde el motor de vídeo de Adobe (AVE).

La aplicación del reproductor puede rastrear las advertencias de reproducción y los errores generados por el AVE, como los eventos de conmutación por error o de caída de red que no detienen la reproducción y no requieren necesariamente ninguna acción por parte de la aplicación. Aunque algunos errores de AVE los soluciona el TVSDK, `NotificationEvent` sirve como mecanismo de paso a través general de la capa de aplicación para advertencias AVE. Después de recibir advertencias de AVE, puede optar por realizar algunas acciones, como detener la reproducción de forma proactiva, activar un plan de contingencia, registrar mensajes, etc.

Utilice los siguientes elementos de API para rastrear advertencias de AVE en el reproductor:

**NotificationCode**

```
public final class NotificationCode { 
    /** 
     * Warning message for playback status. 
     */ 
    public static const GENERAL_WARNING:int = 101100; 
}
```

**NotificationEvent**

```
/** 
 * Event dispatched by MediaPlayer when a notification is available 
 * for the current media stream being played. 
 */ 
public class NotificationEvent extends Event { 
    /** 
     * Event dispatched when a new warning has been received for the current item. 
     * 
     * The newly created Notification object can be accessed through  
     * the notification property of this event. 
     */ 
    public static const WARNING_AVAILABLE:String = "warningAvailable"; 
    /** 
     * Helper method for creating NotificationEvent events. 
     * Throws an ArgumentError if the specified ad break is null. 
     * @param notification Associated notification object. 
     * 
     * @return a valid notification event instance. 
     */ 
    public static function create( 
           type:String, notification:Notification):NotificationEvent; 
     /** 
     * Default constructor 
     * Throws an ArgumentError if the specified ad break is null. 
     * @param type           Event type. 
     * @param bubbles        Whether the event can bubble up the display list hierarchy. 
     * @param cancelable     Whether the behavior associated with the event can be prevented. 
     * @param notification   Associated notification object. 
     */ 
    public function NotificationEvent(type:String,  
                                      bubbles:Boolean=false,  
                                      cancelable:Boolean=false,  
                                      notification:Notification= null); 
     /** 
     * The notification associated with this event. 
     */ 
    public function get notification():Notification; 
    /** 
     * @inheritDoc 
     */ 
    public override function clone():Event; 
}
```

Añada un detector de eventos al reproductor para detectar advertencias de AVE.

Por ejemplo:

```
var _player:DefaultMediaPlayer = new DefaultMediaPlayer(context); 
_player.addEventListener(NotificationEvent.WARNING_AVAILABLE, onWarningAvailable); 
 
private function onWarningAvailable(event:NotificationEvent):void { 
    var metadata:Metadata = event.notification.metadata; 
    if (metadata != null) { 
        for each (var key:String in metadata.keySet()) { 
            var value:String = metadata.getValue(key); 
            if (!StringUtils.isEmpty(key) && !StringUtils.isEmpty(value)) { 
                _logger.warn("#onWarningAvailable metadata [{0}:{1}]", key, value); 
            } 
        } 
    } 
} 
```

<!--<a id="example_C35262605D394718B40C084B569A5052"></a>-->

A continuación, se muestra un ejemplo de advertencias AVE que se rastrearon mediante `NotificationEvent`:

```
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [resourceType:HLS] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [resourceId:0] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [runtimeCode:66] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [runtimeCodeMessage:SEGMENT_SKIPPED_ON_FAILURE] 
[WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [eventType:Warning] 
 
<pre>
  [WARN ] [psdkdemo::PSDKDemo] #onWarningAvailable metadata [description:url::= 
   https://xyz.corp.adobe.com/pmp/assets/abc/failover/tc.1.04/content/backup-01/ 
   low-res/main-stream4-4x3-info6.ts,periodIndex::=0, 
   sizeBytes::=0,downloadTime(ms)::=0,mediaDuration(ms)::=0] 
</pre>
```
