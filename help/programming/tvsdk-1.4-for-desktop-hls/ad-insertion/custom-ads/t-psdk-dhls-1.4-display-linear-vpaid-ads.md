---
description: TVSDK admite la visualización de publicidades de definición de interfaz de publicidad (VPAID) del reproductor de vídeo lineal en una pausa publicitaria. VPAID versión 1.0 requiere Flash, mientras que la versión 2.0 también funciona con TVSDK de explorador y JavaScript.
seo-description: TVSDK admite la visualización de publicidades de definición de interfaz de publicidad (VPAID) del reproductor de vídeo lineal en una pausa publicitaria. VPAID versión 1.0 requiere Flash, mientras que la versión 2.0 también funciona con TVSDK de explorador y JavaScript.
seo-title: Mostrar publicidades VPAID lineales en una pausa publicitaria
title: Mostrar publicidades VPAID lineales en una pausa publicitaria
uuid: 1f3a5426-79f5-49a1-a913-923708c09ade
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Mostrar publicidades VPAID lineales en una pausa publicitaria{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK admite la visualización de publicidades de definición de interfaz de publicidad (VPAID) del reproductor de vídeo lineal en una pausa publicitaria. VPAID versión 1.0 requiere Flash, mientras que la versión 2.0 también funciona con TVSDK de explorador y JavaScript.

Para mostrar las publicidades VPAID correctamente, debe proporcionar un contenedor de publicidad ( `AdContainerView`) dentro de la `MediaPlayerContext` instancia.

Limitaciones para las publicidades VPAID:

* Las publicidades VPAID no necesariamente tienen una duración predefinida, dado que la publicidad puede ser interactiva. Por lo tanto, es posible que la duración de la publicidad (definida por la respuesta del servidor de publicidad) no siempre se corresponda exactamente con la duración real de la publicidad.
* Para anuncios VPAID 1.0, TVSDK requiere Flash Player 14.0.0.160 o bueno instalado en el dispositivo. En versiones anteriores de Flash Player, esta función está desactivada y se omiten las publicidades de VPAID 1.0.

Para configurar un contenedor de publicidad para mostrar publicidades VPAID (versión 1.0 o 2.0) dentro de una pausa publicitaria:

1. Utilice el siguiente código de muestra para configurar un contenedor de publicidad que pueda mostrar publicidades VPAID.

   ```
   var context:MediaPlayerContext =  
     new MediaPlayerContext(_authorizedFeatureHelper.authorizedFeatures); 
   
   adContainer = new AdContainerView(); 
   adContainer.x = adContainer.y = 0; 
   adContainer.setSize(videoContainer.width, videoContainer.height); 
   addChild(adContainer); 
   
   context.adContainer = adContainer; 
   _player = new DefaultMediaPlayer(context);
   ```

1. Cuando cambie el tamaño de la vista, restablezca el tamaño en el contenedor de publicidad.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >Cuando se obtiene un evento de cambio de pantalla completa y se establece el nuevo tamaño en el contenedor de publicidad, se pasa el estado de visualización del escenario de la siguiente manera para garantizar que el reproductor cambia de tamaño correctamente:    >
   >
   >
   ```>
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```   >
   >



