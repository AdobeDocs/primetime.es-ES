---
description: En dispositivos que admiten la aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo directamente en el hardware del dispositivo.
title: Requisitos mínimos de StageVideo
exl-id: f401682d-c47d-4284-8832-293515a76581
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Requisitos mínimos de StageVideo{#stagevideo-minimum-requirements}

En dispositivos que admiten la aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo directamente en el hardware del dispositivo.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

Una combinación de diferentes factores determina cuándo y cómo se puede utilizar `StageVideo`. La siguiente tabla presenta una instantánea de algunos de los requisitos y restricciones asociados con el uso de StageVideo. Estos requisitos y restricciones están sujetos a cambios.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Plataforma </th> 
   <th colname="col2" class="entry"> SO Windows y Mac </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> reproductor de Flash </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">Al menos Flash 10.1 o posterior </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">Para volver a la función de software, Flash 15 y posterior </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Navegadores y <span class="codeph"> wmode</span> configuración </td> 
   <td colname="col2"> <p><b>En el Flash 15</b>, configurado <span class="codeph"> wmode=opaco</span> para poder utilizar superposiciones de HTML. </p> <p>Actualmente, los siguientes exploradores no admiten la aceleración de hardware: 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Mozilla Firefox en Microsoft Windows </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome anterior a 26 y cualquier versión de Chrome en Windows XP y Vista </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer (todas las versiones) </li> 
     </ul>Otras combinaciones de explorador y sistema operativo pueden impedir el acceso a la aceleración de hardware. En estos casos, <span class="codeph"> StageVideo</span> vuelve al software con un impacto negativo en el rendimiento. </p> <p><b>En el Flash 14 y anteriores</b>Sin embargo, si el explorador no admite la aceleración de hardware, el reproductor de Flash puede procesarse directamente en la GPU, pero configurarse <span class="codeph"> wmode=direct</span> para habilitar este procesamiento. <p>Sugerencia: Es posible que sea necesario actualizar los controladores de GPU anteriores a 2009, ya que es posible que no admitan la aceleración de hardware. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Objeto NetStream </td> 
   <td colname="col2">El <span class="codeph"> StageVideoEvent.RENDER_STATE</span> El evento no se enviará a menos que adjunte un <span class="codeph"> NetStream</span> objeto a <span class="codeph"> StageVideo</span> objeto. </td> 
  </tr> 
 </tbody> 
</table>
