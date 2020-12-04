---
description: Puede configurar nombres de etiquetas personalizados en TVSDK de forma global con la clase MediaPlayerItemConfig.
seo-description: Puede configurar nombres de etiquetas personalizados en TVSDK de forma global con la clase MediaPlayerItemConfig.
seo-title: Métodos de clase Config para etiquetas
title: Métodos de clase Config para etiquetas
uuid: f2758085-8e49-4eaf-82bb-4a2e4dd8accb
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Métodos de clase Config para etiquetas{#config-class-methods-for-tags}

Puede configurar nombres de etiquetas personalizados en TVSDK de forma global con la clase MediaPlayerItemConfig.

TVSDK aplica la configuración global automáticamente a cualquier flujo de medios que no especifique una configuración específica del flujo.

`MediaPlayerItemConfig` expone estos métodos para administrar las etiquetas personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Suscripción a etiquetas personalizadas específicas</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags()  </span> </td> 
   <td colname="col2"> Recupera la lista actual de las etiquetas suscritas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(etiquetas String[]);  </span> </td> 
   <td colname="col2"> Establece la lista de las etiquetas suscritas que se expondrán a la aplicación. <p>La aplicación también se suscribe automáticamente a todas las etiquetas transmitidas a través de <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Personalización de las etiquetas de publicidad utilizadas por el detector de oportunidades predeterminado</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags();  </span> </td> 
   <td colname="col2"> Recupera la lista actual de las etiquetas de publicidad. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(etiquetas String[]);  </span> </td> 
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

