---
description: Puede configurar globalmente nombres de etiquetas personalizados en TVSDK con la clase MediaPlayerItemConfig.
title: Métodos de clase de configuración para etiquetas
exl-id: 48e88284-788c-49b3-a370-3e3d77a8da6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Métodos de clase de configuración para etiquetas {#config-class-methods-for-tags}

Puede configurar globalmente nombres de etiquetas personalizados en TVSDK con la clase MediaPlayerItemConfig.

TVSDK aplica automáticamente la configuración global a cualquier flujo de medios que no especifique una configuración específica del flujo.

`MediaPlayerItemConfig` expone estos métodos para administrar las etiquetas personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Suscripción a etiquetas personalizadas específicas</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags </span> </td> 
   <td colname="col2"> <p>Recupera la lista actual de etiquetas suscritas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(String[] tags); </span> </td> 
   <td colname="col2"> <p>Establece la lista de etiquetas suscritas que se expondrán a la aplicación. </p> <p>Su aplicación también se suscribe automáticamente a todas las etiquetas transmitidas a través de <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalizar las etiquetas de anuncio utilizadas por el detector de oportunidades predeterminado</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags; </span> </td> 
   <td colname="col2"> <p>Recupera la lista actual de etiquetas de publicidad. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(String[] tags); </span> </td> 
   <td colname="col2"> <p>Establece la lista de etiquetas de publicidad que se utilizarán en el generador de oportunidades predeterminado. </p> </td> 
  </tr> 
 </tbody> 
</table>

Recuerde lo siguiente:

* Los métodos del establecedor no permiten que el parámetro de etiquetas contenga valores nulos.

   Si se encuentra, TVSDK genera un `IllegalArgumentException`.
* El nombre de etiqueta personalizado debe contener la variable `#` prefijo.

   Por ejemplo, `#EXT-X-ASSET` es un nombre de etiqueta personalizado correcto, pero `EXT-X-ASSET` es incorrecto.

* No puede cambiar la configuración después de cargar el flujo de medios.
