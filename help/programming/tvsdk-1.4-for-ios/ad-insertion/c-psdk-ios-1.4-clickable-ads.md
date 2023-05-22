---
description: TVSDK le proporciona información para que pueda actuar sobre los anuncios en los que se hace clic. A medida que crea la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en un anuncio en el que se puede hacer clic.
title: Anuncios en los que se puede hacer clic
exl-id: eaaab835-884a-4d3f-b3be-e6f71c814985
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Anuncios en los que se puede hacer clic{#clickable-ads}

TVSDK le proporciona información para que pueda actuar sobre los anuncios en los que se hace clic. A medida que crea la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en un anuncio en el que se puede hacer clic.

En TVSDK para iOS, solo se puede hacer clic en anuncios lineales.

## Responder a clics en anuncios {#section_537AF2593FDB4257B81AAE2103B0C719}

Cuando un usuario hace clic en un anuncio, en un anuncio tipo titular o en un botón relacionado, la aplicación debe responder. TVSDK proporciona información sobre la URL de destino para el clic.

1. Para configurar un detector de eventos para TVSDK y proporcionar la información de clics, agregue un observador para `PTMediaPlayerAdClickNotification`.

   >[!NOTE]
   >
   >Cuando un usuario hace clic en un anuncio, en un anuncio tipo titular o en un botón relacionado, TVSDK envía esta notificación, incluida la información sobre el destino del clic.

1. Monitorice las interacciones del usuario con anuncios en los que se puede hacer clic.
1. Cuando el usuario toque o haga clic en el anuncio o el botón, para notificar a TVSDK, utilice `[_player notifyClick:_currentAd.primaryAsset];`.
1. Escuche el `PTMediaPlayerAdClickNotification` de TVSDK.
1. Para recuperar la URL de pulsación y la información relacionada, utilice el `PTMediaPlayerAdClickURLKey` objeto.
1. Pausar el vídeo.
1. Utilice la información de pulsaciones para mostrar la URL de pulsaciones de anuncios y la información relacionada.

   >[!NOTE]
   >
   >Por ejemplo, puede mostrar la información de una de las siguientes maneras:

   * En la aplicación, al abrir la URL de pulsación en un explorador.

      En plataformas de escritorio, el área de reproducción de anuncios de vídeo se utiliza para invocar direcciones URL de pulsación cuando el usuario hace clic.
   * Redirija a los usuarios a su explorador web móvil externo.

      En dispositivos móviles, el área de reproducción de anuncios de vídeo se utiliza para otras funciones, como ocultar y mostrar controles, pausar la reproducción, expandirse a pantalla completa, etc. En estos dispositivos, se utiliza una vista independiente, como un botón patrocinador, para iniciar la URL de pulsación.

1. Cierre la ventana del explorador en la que se muestra la información de pulsaciones y reanude la reproducción del vídeo.

   Por ejemplo:

   ```
      // Listening for click notification  
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdClick:)  
    name:PTMediaPlayerAdClickNotification object:self.player]; 
   - (void) onMediaPlayerAdClick:(NSNotification *) notification { 
      NSString *url = [notification.userInfo objectForKey:PTMediaPlayerAdClickURLKey];  
      if (url != nil) { 
          [self openBrowser:[NSURL URLWithString:url]]; 
      } 
   } 
   ```
