---
description: TVSDK admite la visualización de publicidades de definición de interfaz de publicidad (VPAID) del reproductor de vídeo lineal en una pausa publicitaria. VPAID versión 1.0 requiere Flash, mientras que la versión 2.0 también funciona con Browser TVSDK y JavaScript.
seo-description: TVSDK admite la visualización de publicidades de definición de interfaz de publicidad (VPAID) del reproductor de vídeo lineal en una pausa publicitaria. VPAID versión 1.0 requiere Flash, mientras que la versión 2.0 también funciona con Browser TVSDK y JavaScript.
seo-title: Mostrar publicidades VPAID lineales en una pausa publicitaria
title: Mostrar publicidades VPAID lineales en una pausa publicitaria
uuid: 1f3a5426-79f5-49a1-a913-923708c09ade
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Mostrar publicidades VPAID lineales en una pausa publicitaria{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK admite la visualización de publicidades de definición de interfaz de publicidad (VPAID) del reproductor de vídeo lineal en una pausa publicitaria. VPAID versión 1.0 requiere Flash, mientras que la versión 2.0 también funciona con Browser TVSDK y JavaScript.

Para mostrar las publicidades VPAID correctamente, debe proporcionar un contenedor de publicidad ( `AdContainerView`) dentro de la `MediaPlayerContext` instancia.

Limitaciones para las publicidades VPAID:

* Las publicidades VPAID no necesariamente tienen una duración predefinida, dado que la publicidad puede ser interactiva. Por lo tanto, es posible que la duración de la publicidad (definida por la respuesta del servidor de publicidad) no siempre se corresponda exactamente con la duración real de la publicidad.
* Para anuncios VPAID 1.0, TVSDK requiere que el reproductor Flash 14.0.0.160 o bueno esté instalado en el dispositivo. En versiones anteriores del reproductor de Flash, esta función está desactivada y se omiten las publicidades VPAID 1.0.

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

1. Cuando la vista cambie de tamaño, restablezca el tamaño en el contenedor de publicidad.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >Cuando se obtiene un evento de cambio de pantalla completa y se establece el nuevo tamaño en el contenedor de publicidad, se pasa el estado de visualización del escenario como se indica a continuación para garantizar que el reproductor cambia de tamaño correctamente:
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```

