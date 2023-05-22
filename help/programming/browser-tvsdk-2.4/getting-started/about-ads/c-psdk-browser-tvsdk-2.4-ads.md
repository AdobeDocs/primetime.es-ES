---
description: Cuando se reproduce contenido, el TVSDK del explorador puede mostrar anuncios y pasar información sobre los anuncios al crear el objeto MediaResource.
title: Anuncios
exl-id: a44ad0fa-841f-474b-89f4-39666190231f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Información general {#ads-overview}

Cuando se reproduce contenido, el TVSDK del explorador puede mostrar anuncios y pasar información sobre los anuncios al crear el objeto MediaResource.

Si lo desea, puede llamar a `prepareToPlay` función después de recibir `AdobePSDK.MediaPlayerStatus.INITIALIZED`.

```js
function onStatusChange (event) { 
   switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
        player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
        break; 
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
        player.play(); 
        break; 
   } 
} 
 
var auditudeSettings     = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.domain  = "sample_auditude_domain"; 
auditudeSettings.mediaId = "sample_media_id"; 
auditudeSettings.zoneId  = "sample_zone_id"; 
 
// event handler 
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
 
var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
```

El TVSDK del explorador también proporciona los siguientes eventos específicos de anuncios que puede utilizar en los controladores de eventos para evitar que el contenido se reenvíe rápidamente cuando se reproducen anuncios:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`
* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

Para ver cómo funciona en el marco de trabajo de la interfaz de usuario, especifique la configuración de anuncios de la siguiente manera:

```js
// Using UI Framework 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource: { 
 
            resourceUrl:'Specify Resource Url', 
 
            auditudeSettings: { 
                validMimeTypes: ["application/x-mpeURL"], 
                domain: "Sample_auditude_domain", 
                mediaId:"sample_media_id", 
                zoneID:"sample_zone_id", 
                creativeRepackagingEnabled:true 
            } 
        } 
    } 
}; 
```

Para obtener más información sobre los `AuditudeSettings`, consulte [Metadatos de inserción de publicidad](../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md).
