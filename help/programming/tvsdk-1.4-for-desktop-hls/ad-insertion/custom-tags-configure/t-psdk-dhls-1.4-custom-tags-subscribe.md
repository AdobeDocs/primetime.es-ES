---
description: TVSDK prepara los objetos TimedMetadata para las etiquetas suscritas cada vez que se encuentran estos objetos en el manifiesto de contenido.
title: Suscripción a etiquetas personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Suscripción a etiquetas personalizadas{#subscribe-to-custom-tags}

TVSDK prepara los objetos TimedMetadata para las etiquetas suscritas cada vez que se encuentran estos objetos en el manifiesto de contenido.

Antes de que comience la reproducción, debe suscribirse a las etiquetas.
Para suscribirse a etiquetas, asigne un vector que contenga los nombres de etiqueta personalizados a `subscribedTags` propiedad. Si también debe cambiar las etiquetas de publicidad utilizadas por el generador de oportunidades predeterminado, asigne un vector que contenga los nombres de etiquetas de publicidad personalizados a `adTags` propiedad.

Para recibir notificaciones sobre etiquetas personalizadas en manifiestos HLS:

1. Configure los nombres de etiquetas de publicidad personalizados globalmente asignando un vector que contenga las etiquetas personalizadas a `subscribeTags` in `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Debe incluir la variable `#` cuando se trabaja con secuencias HLS.

   Por ejemplo:

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. Para cambiar globalmente las etiquetas de publicidad que utiliza el generador de oportunidades predeterminado, asigne un vector que contenga los nombres de etiquetas de publicidad personalizados a `adTags` propiedad en `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. Para que la configuración global surta efecto, reemplace el recurso actual.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. Para establecer los nombres de las etiquetas suscritas para un flujo, si es necesario:
   1. Cree una configuración de elemento de reproductor de contenidos.

      >[!TIP]
      >
      >La forma más sencilla es crear una configuración predeterminada de elemento del reproductor de contenidos.

   1. Asignar un vector que contenga las etiquetas personalizadas a `subscribeTags` in `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. Para cambiar las etiquetas de anuncio que utiliza el generador de oportunidades predeterminado en el flujo especificado, asigne un vector que contenga los nombres de etiquetas de anuncio personalizados a `adTags` propiedad en `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Para que los cambios del flujo surtan efecto, al cargar el flujo de medios, utilice la configuración del elemento del reproductor de medios.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
