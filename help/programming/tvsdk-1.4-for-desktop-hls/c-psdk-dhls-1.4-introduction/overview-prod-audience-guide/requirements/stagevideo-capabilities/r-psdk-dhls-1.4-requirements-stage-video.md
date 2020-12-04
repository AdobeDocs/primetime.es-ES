---
description: En dispositivos que admiten aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo directamente en el hardware del dispositivo.
seo-description: En dispositivos que admiten aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo directamente en el hardware del dispositivo.
seo-title: Requisitos mínimos de StageVideo
title: Requisitos mínimos de StageVideo
uuid: 8916dbac-33e0-4efd-8105-9ddbc85f0a3f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# Requisitos mínimos de StageVideo{#stagevideo-minimum-requirements}

En dispositivos que admiten aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo directamente en el hardware del dispositivo.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

Una combinación de diferentes factores determina cuándo y cómo puede utilizar `StageVideo`. La siguiente tabla presenta una instantánea de algunos de los requisitos y restricciones asociados con el uso de StageVideo. Estos requisitos y restricciones están sujetos a cambios.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Plataforma </th> 
   <th colname="col2" class="entry"> Windows y Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash player </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">Al menos Flash 10.1 o posterior </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">Para la función de reserva de software, Flash 15 y posterior </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Exploradores y configuración <span class="codeph"> wmode</span> </td> 
   <td colname="col2"> <p><b>En Flash 15</b>, defina  <span class="codeph"> wmode=</span> opaqueso para que pueda utilizar las superposiciones HTML. </p> <p>Los siguientes exploradores no admiten actualmente la aceleración de hardware: 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Mozilla Firefox en Microsoft Windows </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome antes de 26 y cualquier versión de Chrome en Windows XP y Vista </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer (todas las versiones) </li> 
     </ul>Otras combinaciones de explorador y SO podrían impedir el acceso a la aceleración de hardware. En estos escenarios, <span class="codeph"> StageVideo</span> regresa al software con un impacto negativo en el rendimiento. </p> <p><b>En Flash 14 y versiones anteriores</b>, si el navegador no admite la aceleración de hardware, el reproductor de Flash puede representarse directamente en la GPU, pero establecer  <span class="codeph"> wmode=</span> directpara habilitar esta representación. <p>Sugerencia:  Es posible que sea necesario actualizar los controladores de GPU anteriores a 2009, ya que estos controladores podrían no ser compatibles con la aceleración de hardware. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Objeto NetStream </td> 
   <td colname="col2">El evento <span class="codeph"> StageVideoEvent.RENDER_STATE</span> no se distribuye a menos que se adjunte un objeto <span class="codeph"> NetStream</span> al objeto <span class="codeph"> StageVideo</span>. </td> 
  </tr> 
 </tbody> 
</table>

