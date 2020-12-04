---
description: TVSDK le proporciona información para que pueda actuar en las publicidades de pulsaciones. A medida que cree la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en una publicidad en la que se pueda hacer clic.
seo-description: TVSDK le proporciona información para que pueda actuar en las publicidades de pulsaciones. A medida que cree la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en una publicidad en la que se pueda hacer clic.
seo-title: Publicidades en las que se puede hacer clic
title: Publicidades en las que se puede hacer clic
uuid: dc02cba7-34ad-4c74-9ceb-2fc1050d54aa
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# Publicidades en las que se puede hacer clic{#clickable-ads}

TVSDK le proporciona información para que pueda actuar en las publicidades de pulsaciones. A medida que cree la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en una publicidad en la que se pueda hacer clic.

En TVSDK para iOS, solo se puede hacer clic en las publicidades lineales.

## Responder a los clics en publicidades {#section_537AF2593FDB4257B81AAE2103B0C719}

Cuando un usuario hace clic en una publicidad, en una publicidad tipo titular complementaria o en un botón relacionado, la aplicación debe responder. TVSDK proporciona información sobre la dirección URL de destino del clic.

1. Para configurar un detector de evento para TVSDK y proporcionar la información de pulsaciones, agregue un observador para `PTMediaPlayerAdClickNotification`.

   >[!NOTE]
   >
   >Cuando un usuario hace clic en un anuncio, en un anuncio de titular complementario o en un botón relacionado, TVSDK envía esta notificación, incluida la información sobre el destino del clic.

1. Monitoree las interacciones del usuario en las publicidades en las que se puede hacer clic.
1. Cuando el usuario toque o haga clic en el anuncio o botón, para notificar a TVSDK, utilice `[_player notifyClick:_currentAd.primaryAsset];`.
1. Escuche el evento `PTMediaPlayerAdClickNotification` de TVSDK.
1. Para recuperar la dirección URL de pulsación y la información relacionada, utilice el objeto `PTMediaPlayerAdClickURLKey`.
1. Pause el vídeo.
1. Utilice la información de pulsaciones para mostrar la dirección URL de pulsaciones de publicidad y la información relacionada.

   >[!NOTE]
   >
   >Por ejemplo, puede mostrar la información de una de las siguientes maneras:

   * En la aplicación, abra la dirección URL de pulsación en un navegador.

      En las plataformas de escritorio, el área de reproducción de anuncios de vídeo se utiliza para invocar direcciones URL de pulsaciones a los clics de los usuarios.
   * Redirija a los usuarios a su navegador web móvil externo.

      En dispositivos móviles, el área de reproducción de anuncios de vídeo se utiliza para otras funciones, como ocultar y mostrar controles, pausar la reproducción, expandirse a pantalla completa, etc. En estos dispositivos, se utiliza una vista independiente, como un botón de patrocinador, para iniciar la dirección URL de pulsación.

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

