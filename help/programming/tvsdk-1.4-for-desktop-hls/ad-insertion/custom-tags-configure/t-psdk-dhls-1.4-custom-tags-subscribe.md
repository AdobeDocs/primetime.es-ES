---
description: TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que se encuentran estos objetos en el manifiesto de contenido.
title: Suscripción a etiquetas personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# Suscripción a etiquetas personalizadas{#subscribe-to-custom-tags}

TVSDK prepara objetos TimedMetadata para etiquetas suscritas cada vez que se encuentran estos objetos en el manifiesto de contenido.

Antes de iniciar la reproducción, debe suscribirse a las etiquetas .
Para suscribirse a etiquetas, asigne un vector que contenga los nombres de etiqueta personalizados a la propiedad `subscribedTags` . Si también necesita cambiar las etiquetas de publicidad utilizadas por el generador de oportunidades predeterminado, asigne un vector que contenga los nombres de etiqueta de publicidad personalizados a la propiedad `adTags` .

Para recibir notificaciones sobre etiquetas personalizadas en manifiestos HLS:

1. Defina los nombres de las etiquetas de anuncio personalizadas de forma global asignando un vector que contenga las etiquetas personalizadas a `subscribeTags` en `MediaPlayerItemConfig`.

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

1. Para cambiar globalmente las etiquetas de publicidad que usa el generador de oportunidades predeterminado, asigne un vector que contenga los nombres de etiquetas de publicidad personalizadas a la propiedad `adTags` en `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. Para que todos los ajustes globales tengan efecto, reemplace el recurso actual.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. Para definir los nombres de las etiquetas suscritas para una secuencia, si es necesario:
   1. Cree una configuración de elemento del reproductor de medios.

      >[!TIP]
      >
      >La forma más sencilla es crear una configuración de elemento predeterminada del reproductor de medios.

   1. Asigne un vector que contenga las etiquetas personalizadas a `subscribeTags` en `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. Para cambiar las etiquetas de publicidad que usa el generador de oportunidades predeterminado en el flujo especificado, asigne un vector que contenga los nombres de etiquetas de publicidad personalizadas a la propiedad `adTags` en `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Para que los cambios del flujo surtan efecto, al cargar el flujo de medios, utilice la configuración del elemento del reproductor de medios.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

