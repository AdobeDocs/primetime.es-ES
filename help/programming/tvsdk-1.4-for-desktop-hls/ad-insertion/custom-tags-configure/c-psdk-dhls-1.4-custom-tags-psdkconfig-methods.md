---
description: Puede configurar nombres de etiquetas personalizados en TVSDK de forma global con la clase MediaPlayerItemConfig o basada en flujo con la clase MediaPlayerItemConfig.
seo-description: Puede configurar nombres de etiquetas personalizados en TVSDK de forma global con la clase MediaPlayerItemConfig o basada en flujo con la clase MediaPlayerItemConfig.
seo-title: Métodos de clase Config para etiquetas
title: Métodos de clase Config para etiquetas
uuid: 3317fc8b-c13c-4e7d-8334-aa8cdf40fa05
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Métodos de clase Config para etiquetas{#config-class-methods-for-tags}

Puede configurar nombres de etiquetas personalizados en TVSDK de forma global con la clase MediaPlayerItemConfig o basada en flujo con la clase MediaPlayerItemConfig.

TVSDK aplica la configuración global automáticamente a cualquier flujo de medios que no especifique una configuración específica del flujo.

Tanto `PSDKConfig` como `MediaPlayerItemConfig` exponen estos métodos para administrar las etiquetas personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>Suscripción a etiquetas personalizadas específicas</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> función pública get subscriptionTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> Recupera la lista actual de las etiquetas suscritas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> función pública set subscripTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2">Establece la lista de las etiquetas suscritas que se expondrán a la aplicación. <p>La aplicación también se suscribe automáticamente a todas las etiquetas transmitidas a través de <span class="codeph"> adTags</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>Personalización de las etiquetas de publicidad utilizadas por el detector de oportunidades predeterminado  </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> función pública get adTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> Recupera la lista actual de las etiquetas de publicidad. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function set adTags():Vector.&lt;string&gt;</span> </td> 
   <td colname="col2"> Establece la lista de las etiquetas de publicidad que se utilizarán en el generador de oportunidades predeterminado. </td> 
  </tr> 
 </tbody> 
</table>

Recuerde lo siguiente:

* Los métodos setter no permiten que el parámetro tags contenga valores nulos.

   Si se encuentra, TVSDK emite un `IllegalArgumentException`.
* El nombre de etiqueta personalizado debe contener el prefijo #.

   Por ejemplo, `#EXT-X-ASSET` es un nombre de etiqueta personalizado correcto, pero `EXT-X-ASSET` es incorrecto.
* No puede cambiar la configuración después de cargar el flujo de medios.

