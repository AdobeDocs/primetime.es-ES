---
description: TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.
seo-description: TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.
seo-title: Suscripción a etiquetas personalizadas
title: Suscripción a etiquetas personalizadas
uuid: 43480265-4951-466a-a347-6debfb6935ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Suscripción a etiquetas personalizadas{#subscribe-to-custom-tags}

TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que estos objetos se encuentran en el manifiesto de contenido.

Antes de los inicios de reproducción, debe suscribirse a las etiquetas.
Para suscribirse a etiquetas, asigne un vector que contenga los nombres de etiqueta personalizados a la propiedad `subscribedTags`. Si también necesita cambiar las etiquetas de publicidad utilizadas por el generador de oportunidades predeterminado, asigne un vector que contenga los nombres de etiquetas de publicidad personalizados a la propiedad `adTags`.

Para recibir notificaciones sobre las etiquetas personalizadas en los manifiestos HLS:

1. Configure los nombres de etiquetas de publicidad personalizados de forma global asignando un vector que contenga las etiquetas personalizadas a `subscribeTags` en `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Debe incluir el prefijo `#` al trabajar con flujos HLS.

   Por ejemplo:

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. Para cambiar globalmente las etiquetas de publicidad que utiliza el generador de oportunidades predeterminado, asigne un vector que contenga los nombres de etiquetas de publicidad personalizados a la propiedad `adTags` en `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. Para que todos los ajustes globales tengan efecto, reemplace el recurso actual.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. Para definir los nombres de etiquetas suscritas para un flujo, si es necesario:
   1. Cree una configuración de elemento de reproductor multimedia.

      >[!TIP]
      >
      >La forma más sencilla es crear una configuración de elemento de reproductor de medios predeterminada.

   1. Asigne un vector que contenga las etiquetas personalizadas a `subscribeTags` en `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. Para cambiar las etiquetas de publicidad que utiliza el generador de oportunidades predeterminado en el flujo especificado, asigne un vector que contenga los nombres de etiquetas de publicidad personalizados a la propiedad `adTags` en `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Para que los cambios del flujo surtan efecto, al cargar el flujo de medios, utilice la configuración del elemento del reproductor de medios.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

