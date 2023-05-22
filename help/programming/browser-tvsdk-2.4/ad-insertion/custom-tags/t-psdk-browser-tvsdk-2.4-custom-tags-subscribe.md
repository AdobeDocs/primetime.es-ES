---
description: TVSDK del explorador prepara los objetos TimedMetadata para las etiquetas suscritas cada vez que se encuentran estos objetos en el archivo de descripción de presentación de medios (MPD).
title: Suscripción a etiquetas de publicidad personalizadas
exl-id: d4b9ec3a-9c3f-4adf-984e-b45862e97140
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Suscripción a etiquetas de publicidad personalizadas{#subscribe-to-custom-ad-tags}

TVSDK del explorador prepara los objetos TimedMetadata para las etiquetas suscritas cada vez que se encuentran estos objetos en el archivo de descripción de presentación de medios (MPD).

Debe suscribirse a las etiquetas antes de que comience la reproducción.
Para suscribirse a etiquetas, establezca un vector que contenga los nombres de etiqueta personalizados en `subscribedTags` propiedad. Si también necesita cambiar las etiquetas de publicidad utilizadas por el generador de oportunidades predeterminado, establezca un vector que contenga los nombres de las etiquetas de publicidad personalizadas en `adTags` propiedad.

Para suscribirse a etiquetas personalizadas:

1. Cree una nueva configuración de elemento del reproductor de contenidos.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. Cree un vector de cadena vacío.

   ```js
   var subscribeTags = [];
   ```

1. Añada los nombres de etiquetas personalizados a este vector.

   >[!IMPORTANT]
   >
   >Si está tratando con flujos HLS, recuerde incluir el `#` prefijo.

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. Asigne el vector actualizado a `mediaPlayerItemConfig.subscribeTags` propiedad.

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. Cree un vector de cadena vacío.

   ```js
   var adTags= [];
   ```

1. Añada el nombre de etiqueta de anuncio personalizado a este vector.

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. Asigne el vector actualizado a `mediaPlayerItemConfig.adTags` propiedad.

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Utilice la configuración del elemento del reproductor de contenidos al cargar el flujo de contenidos.

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```
