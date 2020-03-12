---
description: Puede configurar nombres de etiquetas personalizados en un flujo con la clase MediaPlayerItemConfig.
seo-description: Puede configurar nombres de etiquetas personalizados en un flujo con la clase MediaPlayerItemConfig.
seo-title: Métodos de clase Config para etiquetas
title: Métodos de clase Config para etiquetas
uuid: 222a0349-58d5-4bf3-9d03-e5920610faf5
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661

---


# Métodos de clase Config para etiquetas{#config-class-methods-for-tags}

Puede configurar nombres de etiquetas personalizados en un flujo con la clase MediaPlayerItemConfig.

To create a new `MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

A continuación se proporciona información sobre cómo se utilizan los `MediaPlayerItemConfig` métodos para administrar las etiquetas personalizadas:

<table id="table_0AC0973497144DDAB05726E3F031ACD1"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Suscripción a etiquetas personalizadas específicas</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;subscribeTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Recupera la lista actual de etiquetas suscritas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Establece la lista de etiquetas suscritas expuestas a la aplicación. </p> <p>La aplicación también se suscribe automáticamente a todas las etiquetas que se transmiten a través de <span class="codeph"> las etiquetas de publicidad </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalización de las etiquetas de publicidad utilizadas por el detector de oportunidades predeterminado </b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;adTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.adTags; 
    </code> </td> 
   <td colname="col2"> <p>Recupera la lista actual de etiquetas de publicidad. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>Establece la lista de etiquetas de publicidad que usará el generador de oportunidades predeterminado. </p> </td> 
  </tr> 
 </tbody> 
</table>

Recuerde lo siguiente:

* El nombre de la etiqueta personalizada debe contener el `#` prefijo.

   Por ejemplo, `#EXT-X-ASSET` es un nombre de etiqueta personalizado correcto, pero `EXT-X-ASSET` es incorrecto.

* No puede cambiar la configuración después de cargar el flujo de medios.

