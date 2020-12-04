---
description: Compruebe las restricciones y los requisitos de los flujos y listas de reproducción (manifiestos).
seo-description: Compruebe las restricciones y los requisitos de los flujos y listas de reproducción (manifiestos).
seo-title: Requisitos de contenido y manifiesto
title: Requisitos de contenido y manifiesto
uuid: 22ee7d02-b06d-4162-a8a4-a2391658fdb3
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Requisitos de contenido y manifiesto{#content-and-manifest-requirements}

Compruebe las restricciones y los requisitos de los flujos y listas de reproducción (manifiestos).

<table id="table_D7C38CD3B4D24C3D9A3B55D8CEFE7366"> 
 <tbody> 
  <tr> 
   <td colname="col1"> Duración del segmento de contenido </td> 
   <td colname="col2"> La duración de un segmento no debe superar la duración del destinatario especificada en el archivo de manifiesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Requisito de contenido </td> 
   <td colname="col2"> Cada segmento de TS debe tener un inicio con un marco clave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Contenido de HLS </td> 
   <td colname="col2"> <p>Recuerde lo siguiente: 
     <ul id="ul_B226605345EA46F69DA1380E16826117"> 
      <li id="li_6564DC0E879544BB8513DD2D1CFBA8DE">No se admite audio AAC-SSR. </li> 
      <li id="li_B73CAEBE4347406EA4DB25551B444BDA">Los códecs de audio AC3 y AC3 mejorado no son compatibles. </li> 
      <li id="li_5986DD33C0FE485D99D4C00E2E6012CA">Los flujos HLS con discontinuidad, pero no se admiten marcadores de discontinuidad. </li> 
      <li id="li_FED8686372DF4A39BAABC531BA4EB137">HLS Live no admite el rollover de marca de hora. </li> 
      <li id="li_565CFBEAD9874BA48F6E25B0893BF131">Los anuncios de la ventana DVR de los flujos HLS Live no se resuelven. </li> 
      <li id="li_7D22EA32C94240D79EDDA96D9E72FE8F">El rango de bytes no es compatible con el contenido cifrado AES-128. </li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Contenido de DASH </td> 
   <td colname="col2"> <p>Recuerde lo siguiente: 
     <ul id="ul_9D33C2418F9F49DEAE0E642301726F89"> 
      <li id="li_74C69A21A7BD4831B92F0D57900E1CB1">Para flujos en directo: se admite el perfil en directo con tipo dinámico. </li> 
      <li id="li_0C8743DB152047819D23C9F180998AD7">Para flujos VOD: se admite el perfil activo con tipo estático. </li> 
      <li id="li_FBC6828663FB413798A4BDAF0B9831AA">Para flujos de VOD: el perfil a petición no está certificado para flujos de trabajo de publicidad. </li> 
      <li id="li_4393B9B1F6144BDEAE484C879750ED23">No se admite la reproducción de flujos DASH con varios períodos. </li> 
      <li id="li_6A2CEC4E974C4D44A45F5503A1A9D8D0">Se admiten los rótulos incrustados (608/708), marcados mediante la etiqueta Accesibilidad. </li> 
      <li id="li_EDE93DF4F3A64A53BA80877F701A8F0D">No se admiten los archivos VTT fragmentados o segmentados. </li> 
      <li id="li_8897F73611194030A490A4FF1178364C">Los flujos con etiquetas personalizadas dentro de banda no están certificados. </li> 
     </ul></p> </td> 
  </tr> 
 </tbody> 
</table>

