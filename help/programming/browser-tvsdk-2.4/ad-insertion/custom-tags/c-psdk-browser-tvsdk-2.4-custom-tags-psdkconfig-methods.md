---
description: Puede configurar nombres de etiquetas personalizados en una secuencia con la clase MediaPlayerItemConfig.
title: Métodos de clase de configuración para etiquetas
exl-id: 864d5c35-2b26-447b-8134-414e82096f18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Métodos de clase de configuración para etiquetas{#config-class-methods-for-tags}

Puede configurar nombres de etiquetas personalizados en una secuencia con la clase MediaPlayerItemConfig.

Para crear un nuevo `MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

A continuación se proporciona información sobre cómo `MediaPlayerItemConfig` Los métodos de se utilizan para administrar etiquetas personalizadas:

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
   <td colname="col2"> <p>Establece la lista de etiquetas suscritas expuestas a la aplicación. </p> <p>Su aplicación también se suscribe automáticamente a todas las etiquetas que se transmiten a través de <span class="codeph"> adTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizar las etiquetas de anuncio utilizadas por el detector de oportunidades predeterminado </b> </td> 
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
   <td colname="col2"> <p>Establece la lista de etiquetas de publicidad que utilizará el generador de oportunidades predeterminado. </p> </td> 
  </tr> 
 </tbody> 
</table>

Recuerde lo siguiente:

* El nombre de etiqueta personalizado debe contener la variable `#` prefijo.

   Por ejemplo, `#EXT-X-ASSET` es un nombre de etiqueta personalizado correcto, pero `EXT-X-ASSET` es incorrecto.

* No puede cambiar la configuración después de cargar el flujo de medios.
