---
description: Cuando un usuario hace clic en una publicidad o en un botón relacionado, la aplicación debe responder. TVSDK proporciona información sobre la dirección URL de destino del clic.
seo-description: Cuando un usuario hace clic en una publicidad o en un botón relacionado, la aplicación debe responder. TVSDK proporciona información sobre la dirección URL de destino del clic.
seo-title: Responder a los clics en publicidades
title: Responder a los clics en publicidades
uuid: abc5de2f-3ab0-4e00-908c-ea8b31387d4f
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc

---


# Responder a los clics en publicidades {#respond-to-clicks-on-ads}

TVSDK le proporciona información para que pueda actuar en las publicidades de pulsaciones. A medida que cree la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en una publicidad en la que se pueda hacer clic.

Para TVSDK para Android, solo se puede hacer clic en las publicidades lineales.
Cuando un usuario hace clic en una publicidad o en un botón relacionado, la aplicación debe responder. TVSDK proporciona información sobre la dirección URL de destino del clic.

1. Para configurar un detector de eventos para TVSDK y proporcionar la información de pulsaciones, regístrese `AdClickedEventListener.onAdClicked`.

   Cuando un usuario hace clic en un anuncio o en un botón relacionado, TVSDK distribuye esta notificación, incluida la información sobre el destino del clic.
1. Monitoree las interacciones del usuario en las publicidades en las que se puede hacer clic.
1. Cuando el usuario toque o haga clic en el anuncio o botón, para notificar a TVSDK, llame `notifyClick` al `MediaPlayerView`.
1. Escuche el `onAdClick(AdClickEvent event)` evento desde TVSDK.
1. Para recuperar la dirección URL de pulsación y la información relacionada, utilice los métodos de captador para la `AdClickEvent` instancia.
1. Pause el vídeo.

   Para obtener más información sobre la pausa del vídeo, consulte [Pausa y reanudación de la reproducción](../../ad-insertion/clickable-ads/android-3x-pausing-resuming-playback.md).
1. Utilice la información de pulsaciones para mostrar la dirección URL de pulsaciones de publicidad y la información relacionada. Por ejemplo, puede mostrar la información de una de las siguientes maneras:

   * En la aplicación, abra la URL de pulsación en un explorador.

      En las plataformas de escritorio, el área de reproducción de anuncios de vídeo se utiliza para invocar direcciones URL de pulsaciones a los clics de los usuarios.
   * Redirija a los usuarios a su navegador web móvil externo.

      En dispositivos móviles, el área de reproducción de anuncios de vídeo se utiliza para otras funciones, como ocultar y mostrar controles, pausar la reproducción, expandirse a pantalla completa, etc. En estos dispositivos, se utiliza una vista independiente, como un botón de patrocinador, para iniciar la dirección URL de pulsación.

1. Cierre la ventana del explorador en la que se muestra la información de pulsaciones y reanude la reproducción del vídeo.

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

Por ejemplo:

```java
private AdStartedEventListener adStartedEventListener =  
  new AdStartedEventListener() { 
    @Override 
    public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        if (ad == null) { 
            return; 
        } 
 
        _pubOverlay.startAd(adPlaybackEvent.getAdBreak(), ad); 
 
        if (areClickableAdsEnabled() && ad.isClickable()) { 
            _isClickableAdPlaying = true; 
            _playerClickableAdFragment.show(); 
        } 
    } 
}; 
 
private AdCompletedEventListener adCompletedEventListener =  
  new AdCompletedEventListener() { 
    @Override 
    public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        _pubOverlay.stopAd(adPlaybackEvent.getAdBreak(), ad); 
 
        _isClickableAdPlaying = false; 
        if (ad.isClickable()) { 
            _playerClickableAdFragment.hide(); 
        } 
    } 
}; 
 
private AdClickedEventListener adClickedEventListener =  
  new AdClickedEventListener() { 
    @Override 
    public void onAdClicked(AdClickEvent adClickEvent) { 
        AdClick adClick = adClickEvent.getAdClick(); 
        Ad ad = adClickEvent.getAd(); 
 
        String url = adClick.getUrl(); 
        if (url == null || url.trim().equals("")) { 
        } else { 
            Uri uri = Uri.parse(url); 
            Intent intent = new Intent(ACTION_VIEW, uri); 
            try { 
                startActivity(intent); 
            } catch (Exception e) { 
            } 
        } 
    } 
}; 
```
