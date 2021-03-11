---
description: En los dispositivos compatibles con la aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar el vídeo directamente en el hardware del dispositivo.
title: Requisitos mínimos de StageVideo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Requisitos mínimos de StageVideo{#stagevideo-minimum-requirements}

En los dispositivos compatibles con la aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar el vídeo directamente en el hardware del dispositivo.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

Una combinación de diferentes factores determina cuándo y cómo puede usar `StageVideo`. La siguiente tabla presenta una instantánea de algunos de los requisitos y restricciones asociados con el uso de StageVideo. Estos requisitos y restricciones están sujetos a cambios.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Plataforma </th> 
   <th colname="col2" class="entry"> Windows y Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> reproductor de Flash </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">Flash 10.1 o posterior </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">Para la alternativa a la función de software, Flash 15 y posterior </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Configuración de los navegadores y <span class="codeph"> wmode</span> </td> 
   <td colname="col2"> <p><b>En el Flash 15</b>, establezca  <span class="codeph"> wmode=</span> opaqueso para que pueda utilizar las superposiciones HTML. </p> <p>Actualmente, los siguientes exploradores no admiten la aceleración de hardware: 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Mozilla Firefox en Microsoft Windows </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome antes de 26 y cualquier versión de Chrome en Windows XP y Vista </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer (todas las versiones) </li> 
     </ul>Otras combinaciones de navegador/sistema operativo podrían impedir el acceso a la aceleración de hardware. En estos escenarios, <span class="codeph"> StageVideo</span> vuelve al software con un impacto negativo en el rendimiento. </p> <p><b>En el Flash 14 y versiones anteriores</b>, si el navegador no admite la aceleración de hardware, el reproductor de Flash puede procesarse directamente en la GPU, pero establecer  <span class="codeph"> wmode=</span> directpara habilitar esta renderización. <p>Sugerencia:  Es posible que sea necesario actualizar los controladores GPU anteriores a 2009, ya que estos controladores podrían no ser compatibles con la aceleración de hardware. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Objeto NetStream </td> 
   <td colname="col2">El evento <span class="codeph"> StageVideoEvent.RENDER_STATE</span> no se envía a menos que se adjunte un objeto <span class="codeph"> NetStream</span> al objeto <span class="codeph"> StageVideo</span>. </td> 
  </tr> 
 </tbody> 
</table>

