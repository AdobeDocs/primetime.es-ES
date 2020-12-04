---
description: La reproducción en evento completo (FER) es un recurso de VOD que actúa como recurso de vídeo/DVR, por lo que la aplicación debe tomar los pasos necesarios para garantizar que los anuncios se coloquen correctamente.
seo-description: La reproducción en evento completo (FER) es un recurso de VOD que actúa como recurso de vídeo/DVR, por lo que la aplicación debe tomar los pasos necesarios para garantizar que los anuncios se coloquen correctamente.
seo-title: Habilitar publicidades en reproducción de evento completo
title: Habilitar publicidades en reproducción de evento completo
uuid: a8859db1-1408-4365-bf12-5bc2ab7df449
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Habilitar publicidades en reproducción de evento completo {#enable-ads-in-full-event-replay}

La reproducción en evento completo (FER) es un recurso de VOD que actúa como recurso de vídeo/DVR, por lo que la aplicación debe tomar los pasos necesarios para garantizar que los anuncios se coloquen correctamente.

Para el contenido en directo, TVSDK utiliza los metadatos/indicaciones del manifiesto para determinar dónde colocar los anuncios. Sin embargo, a veces el contenido en directo o lineal puede parecerse al contenido de VOD. Por ejemplo, cuando se completa el contenido activo, se agrega una etiqueta `EXT-X-ENDLIST` al manifiesto activo. Para HLS, la etiqueta `EXT-X-ENDLIST` significa que el flujo es un flujo VOD. Para insertar correctamente anuncios, TVSDK no puede diferenciar automáticamente este flujo de un flujo de VOD típico.

La aplicación debe indicar a TVSDK si el contenido está activo o VOD especificando `AdSignalingMode`.

Para un flujo FER, el servidor de decisiones de anuncios de Adobe Primetime no debe proporcionar la lista de pausas publicitarias que deben insertarse en la línea de tiempo antes de iniciar la reproducción. Este es el proceso habitual para el contenido de VOD. En su lugar, al especificar un modo de señalización diferente, TVSDK lee todos los puntos de referencia del manifiesto FER y va al servidor de publicidad para cada punto de referencia para solicitar una pausa publicitaria. Este proceso es similar al contenido en directo/DVR.

>[!TIP]
>
>Además de cada solicitud asociada a un punto de referencia, TVSDK realiza una solicitud de publicidad adicional para anuncios previos.

1. Desde un origen externo, como vCMS, obtenga el modo de señalización que debe utilizarse.
1. Cree los metadatos relacionados con la publicidad.
1. Si se debe sobrescribir el comportamiento predeterminado, especifique `AdSignalingMode` mediante `AdvertisingMetadata.setSignalingMode`.

   Los valores válidos son `DEFAULT`, `SERVER_MAP` y `MANIFEST_CUES`.

   >[!IMPORTANT]
   >
   >Debe establecer el modo de señalización de publicidad antes de llamar a `prepareToPlay`. Tras los inicios de TVSDK para resolver y colocar anuncios en la línea de tiempo, se omiten los cambios en el modo de señalización de publicidad. Establezca el modo cuando cree el objeto `AuditudeSettings`.

1. Continúe con la reproducción.

<!--<a id="example_6DECA71C3C3B4551805C09A80686552F"></a>-->

```java
MediaPlayer mediaPlayer =  
  new MediaPlayer(getActivity.().getApplicationContext()); 
 
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings.setSignalingMode(AdSignalingMode.MANIFEST_CUES); 
auditudeSettings.setDomain("your-auditude-domain"); 
auditudeSettings.setZoneId("your-auditude-zone-id"); 
auditudeSettings.setMediaId("your-media-id"); 
// set additional targeting parameters or custom parameters 
 
MediaPlayerItemConfig itemConfig =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
MediaResource mediaResource =  
  new MediaResource("https://example.com/media/test_media.m3u8",  
                    MediaResource.Type.HLS, Metadata); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (status == MediaPlayerStatus.INITIALIZED) { 
            mediaPlayer.prepareToPlay(); 
        } 
        else if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
            // TVSDK is in the PREPARED state, so start the playback 
            mediaPlayer.play(); 
        } 
        else if( event.getStatus() == MediaPlayerStatus.COMPLETE ) { 
            // playback has reached the end of stream ( ads included ) 
            // if we want to rewind we can call 
            mediaPlayer.seek(mediaPlayer.getSeekableRange().getBegin()); 
        } 
    } 
}); 
 
mediaPlayer.replaceCurrentResource(mediaResource, itemConfig); 
```
