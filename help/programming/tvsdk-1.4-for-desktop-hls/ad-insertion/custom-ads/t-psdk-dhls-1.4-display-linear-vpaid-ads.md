---
description: TVSDK admite la visualización de anuncios lineales de Definición de interfaz de anuncio y reproductor de vídeo (VPAID) en una pausa publicitaria. La versión 1.0 de VPAID requiere Flash, mientras que la versión 2.0 también funciona con el explorador TVSDK y JavaScript.
title: Mostrar anuncios VPAID lineales en una pausa publicitaria
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Mostrar anuncios VPAID lineales en una pausa publicitaria{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK admite la visualización de anuncios lineales de Definición de interfaz de anuncio y reproductor de vídeo (VPAID) en una pausa publicitaria. La versión 1.0 de VPAID requiere Flash, mientras que la versión 2.0 también funciona con el explorador TVSDK y JavaScript.

Para mostrar correctamente los anuncios VPAID, debe proporcionar un contenedor de anuncios ( `AdContainerView`) dentro de `MediaPlayerContext` ejemplo.

Limitaciones para los anuncios VPAID:

* Los anuncios VPAID no tienen necesariamente una duración predefinida, dado que el anuncio puede ser interactivo. Por lo tanto, es posible que la duración de la publicidad (definida por la respuesta del servidor de publicidad) no siempre se corresponda exactamente con la duración real de la publicidad.
* Para los anuncios de VPAID 1.0, TVSDK requiere la instalación del reproductor de Flash 14.0.0.160 o superior en el dispositivo. Para versiones anteriores de Flash Player, esta función está desactivada y se omiten los anuncios VPAID 1.0.

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

1. Cuando cambie el tamaño de la vista, restablezca el tamaño en el contenedor de anuncios.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >Cuando reciba un evento de cambio de pantalla completa y establezca el nuevo tamaño en el contenedor de publicidad, pase el estado de visualización del escenario de la siguiente manera para asegurarse de que el reproductor cambia de tamaño correctamente:
   >
   >```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```
   >
