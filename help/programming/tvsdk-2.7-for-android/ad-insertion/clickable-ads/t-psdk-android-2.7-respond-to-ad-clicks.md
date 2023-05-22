---
description: Cuando un usuario hace clic en un anuncio o en un botón relacionado, la aplicación debe responder. TVSDK proporciona información sobre la URL de destino para el clic.
title: Responder a clics en anuncios
exl-id: a313bb03-a857-48b6-ace7-b61574dbf75f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Responder a clics en anuncios {#respond-to-clicks-on-ads}

TVSDK le proporciona información para que pueda actuar sobre los anuncios en los que se hace clic. A medida que crea la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en un anuncio en el que se puede hacer clic.

Para TVSDK para Android, solo se puede hacer clic en los anuncios lineales.
Cuando un usuario hace clic en un anuncio o en un botón relacionado, la aplicación debe responder. TVSDK proporciona información sobre la URL de destino para el clic.

1. Para configurar un detector de eventos para TVSDK y proporcionar la información de clics, regístrese `AdClickedEventListener.onAdClicked`.

   Cuando un usuario hace clic en un anuncio o en un botón relacionado, TVSDK envía esta notificación, incluida la información sobre el destino del clic.
1. Monitorice las interacciones del usuario con anuncios en los que se puede hacer clic.
1. Cuando el usuario toque o haga clic en el anuncio o el botón, para notificar a TVSDK, llame a `notifyClick` en el `MediaPlayerView`.
1. Escuche el `onAdClick(AdClickEvent event)` de TVSDK.
1. Para recuperar la URL de pulsación y la información relacionada, utilice los métodos de captador para `AdClickEvent` ejemplo.
1. Pausar el vídeo.

   Para obtener más información sobre la pausa del vídeo, consulte pausar-reanudar-reproducción
1. Utilice la información de pulsaciones para mostrar la URL de pulsaciones de anuncios y la información relacionada.

       Por ejemplo, puede mostrar la información de una de las siguientes maneras:
   
   * En la aplicación, abriendo la URL de pulsación en un explorador.

      En plataformas de escritorio, el área de reproducción de anuncios de vídeo se utiliza para invocar direcciones URL de pulsación cuando el usuario hace clic.
   * Redirija a los usuarios a su explorador web móvil externo.

      En dispositivos móviles, el área de reproducción de anuncios de vídeo se utiliza para otras funciones, como ocultar y mostrar controles, pausar la reproducción, expandirse a pantalla completa, etc. En estos dispositivos, se utiliza una vista independiente, como un botón patrocinador, para iniciar la URL de pulsación.

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
