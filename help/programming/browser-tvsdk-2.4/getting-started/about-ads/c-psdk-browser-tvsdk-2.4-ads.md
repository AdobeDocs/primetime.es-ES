---
description: Cuando se reproduce contenido, el SDK de TVSDK del explorador puede mostrar anuncios y pasar información sobre anuncios al crear el objeto MediaResource.
seo-description: Cuando se reproduce contenido, el SDK de TVSDK del explorador puede mostrar anuncios y pasar información sobre anuncios al crear el objeto MediaResource.
seo-title: Publicidades
title: Publicidades
uuid: 9a5e8c83-18ce-41e8-9cb1-fdc9da903faf
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Información general {#ads-overview}

Cuando se reproduce contenido, el SDK de TVSDK del explorador puede mostrar anuncios y pasar información sobre anuncios al crear el objeto MediaResource.

Si lo desea, puede llamar a la `prepareToPlay` función después de recibir `AdobePSDK.MediaPlayerStatus.INITIALIZED`.

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

El SDK de explorador también proporciona los siguientes eventos específicos de publicidad que puede utilizar en los controladores de eventos para evitar que el contenido se reenvíe rápidamente cuando se reproduzcan anuncios:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`
* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

Para ver cómo funciona en la interfaz de usuario, especifique la configuración de la publicidad de la siguiente manera:

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

Para obtener más información sobre los metadatos requeridos `AuditudeSettings`, consulte Metadatos [de inserción](../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md)de anuncios.
