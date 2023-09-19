---
description: Puede configurar los nombres de etiquetas personalizados en TVSDK globalmente con la clase MediaPlayerItemConfig o basados en secuencias con la clase MediaPlayerItemConfig.
title: Métodos de clase de configuración para etiquetas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Métodos de clase de configuración para etiquetas{#config-class-methods-for-tags}

Puede configurar los nombres de etiquetas personalizados en TVSDK globalmente con la clase MediaPlayerItemConfig o basados en secuencias con la clase MediaPlayerItemConfig.

TVSDK aplica la configuración global automáticamente a cualquier flujo de medios que no especifique una configuración específica del flujo.

Ambos `PSDKConfig` y `MediaPlayerItemConfig` exponga estos métodos para administrar las etiquetas personalizadas:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>Suscripción a etiquetas personalizadas específicas</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> función pública get subscribeTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> Recupera la lista actual de etiquetas suscritas. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> la función pública define subscribeTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2">Establece la lista de etiquetas suscritas que se expondrán a la aplicación. <p>Su aplicación también se suscribe automáticamente a todas las etiquetas transmitidas a través de <span class="codeph"> adTags</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>Personalizar las etiquetas de anuncio utilizadas por el detector de oportunidades predeterminado </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> función pública get adTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> Recupera la lista actual de etiquetas de publicidad. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> función pública establecida adTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> Establece la lista de etiquetas de publicidad que se utilizarán en el generador de oportunidades predeterminado. </td> 
  </tr> 
 </tbody> 
</table>

Recuerde lo siguiente:

* Los métodos del establecedor no permiten que el parámetro de etiquetas contenga valores nulos.

  Si se encuentra, TVSDK genera un `IllegalArgumentException`.
* El nombre de etiqueta personalizado debe contener el prefijo #.

  Por ejemplo, `#EXT-X-ASSET` es un nombre de etiqueta personalizado correcto, pero `EXT-X-ASSET` es incorrecto.
* No puede cambiar la configuración después de cargar el flujo de medios.
