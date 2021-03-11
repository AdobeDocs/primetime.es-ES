---
description: El SDK de TVSDK del explorador prepara objetos TimedMetadata para etiquetas suscritas cada vez que se encuentran estos objetos en el archivo de descripción de la presentación de medios (MPD).
title: Suscripción a etiquetas de publicidad personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Suscripción a las etiquetas de publicidad personalizadas{#subscribe-to-custom-ad-tags}

El SDK de TVSDK del explorador prepara objetos TimedMetadata para etiquetas suscritas cada vez que se encuentran estos objetos en el archivo de descripción de la presentación de medios (MPD).

Debe suscribirse a las etiquetas antes de que se inicie la reproducción.
Para suscribirse a etiquetas, establezca un vector que contenga los nombres de etiqueta personalizados en la propiedad `subscribedTags` . Si también necesita cambiar las etiquetas de publicidad utilizadas por el generador de oportunidades predeterminado, establezca un vector que contenga los nombres de etiquetas de publicidad personalizadas en la propiedad `adTags` .

Para suscribirse a etiquetas personalizadas:

1. Cree una nueva configuración de elementos del reproductor de medios.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. Cree un vector de cadena vacío.

   ```js
   var subscribeTags = [];
   ```

1. Agregue los nombres de etiqueta personalizados a este vector.

   >[!IMPORTANT]
   >
   >Si está tratando con flujos HLS, recuerde incluir el prefijo `#`.

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. Asigne el vector actualizado a la propiedad `mediaPlayerItemConfig.subscribeTags` .

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. Cree un vector de cadena vacío.

   ```js
   var adTags= [];
   ```

1. Agregue el nombre de la etiqueta de publicidad personalizada a este vector.

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. Asigne el vector actualizado a la propiedad `mediaPlayerItemConfig.adTags` .

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Utilice la configuración del elemento del reproductor de medios al cargar el flujo de medios.

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```

