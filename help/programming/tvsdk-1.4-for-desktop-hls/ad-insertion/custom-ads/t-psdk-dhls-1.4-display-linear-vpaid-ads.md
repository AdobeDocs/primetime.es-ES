---
description: TVSDK admite la visualización de anuncios de definición de interfaz de anuncios (VPAID) del reproductor de vídeo lineal en una pausa publicitaria. La versión 1.0 de VPAID requiere Flash, mientras que la versión 2.0 también funciona con el TVSDK del explorador y JavaScript.
title: Mostrar anuncios VPAID lineales en una pausa publicitaria
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Mostrar anuncios VPAID lineales en una pausa publicitaria{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK admite la visualización de anuncios de definición de interfaz de anuncios (VPAID) del reproductor de vídeo lineal en una pausa publicitaria. La versión 1.0 de VPAID requiere Flash, mientras que la versión 2.0 también funciona con el TVSDK del explorador y JavaScript.

Para mostrar las publicidades de VPAID correctamente, debe proporcionar un contenedor de anuncios ( `AdContainerView`) dentro de la instancia `MediaPlayerContext` .

Limitaciones para los anuncios VPAID:

* Los anuncios VPAID no necesariamente tienen una duración predefinida, dado que la publicidad puede ser interactiva. Por lo tanto, es posible que la duración de la publicidad (definida por la respuesta del servidor de publicidad) no siempre se corresponda exactamente con la duración real de la publicidad.
* Para los anuncios VPAID 1.0, TVSDK requiere el reproductor de Flash 14.0.0.160 o bueno instalado en el dispositivo. En versiones anteriores del reproductor de Flash, esta función está deshabilitada y los anuncios VPAID 1.0 se omiten.

Para configurar un contenedor de anuncios para mostrar anuncios VPAID (versión 1.0 o 2.0) dentro de una pausa publicitaria:

1. Utilice el siguiente código de ejemplo para configurar un contenedor de anuncios que pueda mostrar anuncios VPAID.

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

1. Cuando la vista cambie de tamaño, restablezca el tamaño en el contenedor de anuncios.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >Cuando se produce un evento de cambio de pantalla completa y se establece el nuevo tamaño en el contenedor de publicidad, pase el estado de visualización del escenario como se indica a continuación para asegurarse de que el reproductor se redimensiona correctamente:
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```

