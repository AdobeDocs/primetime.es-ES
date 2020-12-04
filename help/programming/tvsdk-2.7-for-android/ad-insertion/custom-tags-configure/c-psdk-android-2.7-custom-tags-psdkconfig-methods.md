---
description: Puede configurar de forma global nombres de etiquetas personalizados en TVSDK con la clase MediaPlayerItemConfig.
seo-description: Puede configurar de forma global nombres de etiquetas personalizados en TVSDK con la clase MediaPlayerItemConfig.
seo-title: Métodos de clase Config para etiquetas
title: Métodos de clase Config para etiquetas
uuid: 64284876-1f31-47e0-a99b-3bfe17e10707
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Métodos de clase Config para etiquetas {#config-class-methods-for-tags}

Puede configurar de forma global nombres de etiquetas personalizados en TVSDK con la clase MediaPlayerItemConfig.

TVSDK aplica automáticamente la configuración global a cualquier flujo de medios que no especifique una configuración específica del flujo.

`MediaPlayerItemConfig` expone estos métodos para administrar las etiquetas personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Suscripción a etiquetas personalizadas específicas</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags  </span> </td> 
   <td colname="col2"> <p>Recupera la lista actual de las etiquetas suscritas. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(etiquetas String[]);  </span> </td> 
   <td colname="col2"> <p>Establece la lista de las etiquetas suscritas que se expondrán a la aplicación. </p> <p>La aplicación también se suscribe automáticamente a todas las etiquetas transmitidas a través de <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalización de las etiquetas de publicidad utilizadas por el detector de oportunidades predeterminado</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags;  </span> </td> 
   <td colname="col2"> <p>Recupera la lista actual de las etiquetas de publicidad. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(etiquetas String[]);  </span> </td> 
   <td colname="col2"> <p>Establece la lista de las etiquetas de publicidad que se utilizarán en el generador de oportunidades predeterminado. </p> </td> 
  </tr> 
 </tbody> 
</table>

Recuerde lo siguiente:

* Los métodos setter no permiten que el parámetro tags contenga valores nulos.

   Si se encuentra, TVSDK emite un `IllegalArgumentException`.
* El nombre de etiqueta personalizado debe contener el prefijo `#`.

   Por ejemplo, `#EXT-X-ASSET` es un nombre de etiqueta personalizado correcto, pero `EXT-X-ASSET` es incorrecto.

* No puede cambiar la configuración después de cargar el flujo de medios.
