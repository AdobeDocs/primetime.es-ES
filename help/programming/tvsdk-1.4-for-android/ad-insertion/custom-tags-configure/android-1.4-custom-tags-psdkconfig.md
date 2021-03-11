---
description: Puede configurar nombres de etiquetas personalizados en TVSDK globalmente con la clase MediaPlayerItemConfig .
title: Métodos de clase Config para etiquetas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Métodos de clase Config para etiquetas{#config-class-methods-for-tags}

Puede configurar nombres de etiquetas personalizados en TVSDK globalmente con la clase MediaPlayerItemConfig .

TVSDK aplica la configuración global automáticamente a cualquier flujo de medios que no especifique una configuración específica de flujo.

`MediaPlayerItemConfig` expone estos métodos para administrar las etiquetas personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Suscripción a etiquetas personalizadas específicas</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags()  </span> </td> 
   <td colname="col2"> Recupera la lista actual de etiquetas suscritas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(String[] tags);  </span> </td> 
   <td colname="col2"> Establece la lista de etiquetas suscritas que se expondrán a la aplicación. <p>Su aplicación también se suscribe automáticamente a todas las etiquetas transmitidas a través de <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalización de las etiquetas de publicidad utilizadas por el detector de oportunidades predeterminado</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags();  </span> </td> 
   <td colname="col2"> Recupera la lista actual de etiquetas de publicidad. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(String[] tags);  </span> </td> 
   <td colname="col2"> Establece la lista de etiquetas de publicidad que utilizará el generador de oportunidades predeterminado. </td> 
  </tr> 
 </tbody> 
</table>

Recuerde lo siguiente:

* Los métodos de configuración no permiten que el parámetro de etiquetas contenga valores nulos.

   Si se encuentra, TVSDK lanza un `IllegalArgumentException`.
* El nombre de etiqueta personalizado debe contener el prefijo # .

   Por ejemplo, `#EXT-X-ASSET` es un nombre de etiqueta personalizado correcto, pero `EXT-X-ASSET` no es correcto.
* No puede cambiar la configuración después de cargar el flujo de medios.

