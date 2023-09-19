---
description: La reproducción de evento completo (FER) es un recurso de VOD que actúa como un recurso activo/DVR, por lo que la aplicación debe tomar medidas para garantizar que los anuncios se coloquen correctamente.
title: Habilitar los anuncios en la reproducción de evento completo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Habilitar los anuncios en la reproducción de evento completo {#enable-ads-in-full-event-replay-overview}

La reproducción de evento completo (FER) es un recurso de VOD que actúa como un recurso activo/DVR, por lo que la aplicación debe tomar medidas para garantizar que los anuncios se coloquen correctamente.

Para el contenido en directo, TVSDK utiliza los metadatos y las indicaciones del manifiesto para determinar dónde colocar los anuncios. Sin embargo, a veces el contenido en directo/lineal puede parecerse al contenido de VOD. Por ejemplo, cuando el contenido en directo termina, una `EXT-X-ENDLIST` la etiqueta se anexa al manifiesto en directo. Para HLS, la variable `EXT-X-ENDLIST` significa que el flujo es un flujo de VOD. Para insertar correctamente los anuncios, TVSDK no puede diferenciar automáticamente este flujo de un flujo de VOD típico.

La aplicación debe indicar a TVSDK si el contenido está activo o es VOD especificando la variable `AdSignalingMode`.

Para un flujo FER, el servidor de Adobe Primetime ad Decisioning no debe proporcionar la lista de pausas publicitarias que deben insertarse en la cronología antes de iniciar la reproducción. Este es el proceso típico del contenido de VOD. En su lugar, al especificar un modo de señalización diferente, TVSDK lee todos los puntos de referencia del manifiesto FER y va al servidor de publicidad para cada punto de referencia a fin de solicitar una pausa publicitaria. Este proceso es similar al contenido en directo/DVR.

>[!TIP]
>
>Además de cada solicitud asociada a un punto de referencia, TVSDK realiza una solicitud de anuncio adicional para anuncios previos a la emisión.

1. Desde una fuente externa, como vCMS, obtenga el modo de señalización que debe utilizarse.
1. Cree los metadatos relacionados con la publicidad.
1. Si el comportamiento predeterminado debe sobrescribirse, especifique el `AdSignalingMode` mediante `AdvertisingMetadata.setSignalingMode`.

   Los valores válidos son `DEFAULT`, `SERVER_MAP`, y `MANIFEST_CUES`.

   >[!IMPORTANT]
   >
   >Debe establecer el modo de señalización de anuncio antes de llamar a `prepareToPlay`. Una vez que TVSDK empieza a resolver y a colocar los anuncios en la cronología, se omiten los cambios en el modo de señalización de publicidad. Configure el modo cuando cree la variable `AuditudeSettings` objeto.

1. Continuar con la reproducción.

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
