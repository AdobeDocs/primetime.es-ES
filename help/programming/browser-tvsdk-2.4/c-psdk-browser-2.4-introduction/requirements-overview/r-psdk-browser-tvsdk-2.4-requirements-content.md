---
description: Compruebe las restricciones y los requisitos para emisiones y listas de reproducción (manifiestos).
title: Requisitos de contenido y manifiesto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# Requisitos de contenido y manifiesto{#content-and-manifest-requirements}

Compruebe las restricciones y los requisitos para emisiones y listas de reproducción (manifiestos).

<table id="table_D7C38CD3B4D24C3D9A3B55D8CEFE7366"> 
 <tbody> 
  <tr> 
   <td colname="col1"> Duración del segmento de contenido </td> 
   <td colname="col2"> La duración de un segmento no debe superar la duración de destino especificada en el archivo de manifiesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Requisito de contenido </td> 
   <td colname="col2"> Cada segmento de TS debe comenzar con un fotograma clave. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Contenido HLS </td> 
   <td colname="col2"> <p>Recuerde lo siguiente: 
     <ul id="ul_B226605345EA46F69DA1380E16826117"> 
      <li id="li_6564DC0E879544BB8513DD2D1CFBA8DE">El audio AAC-SSR no es compatible. </li> 
      <li id="li_B73CAEBE4347406EA4DB25551B444BDA">Los códecs de audio AC3 y Enhanced AC3 no son compatibles. </li> 
      <li id="li_5986DD33C0FE485D99D4C00E2E6012CA">El HLS transmite con discontinuidad, pero no admite marcadores de discontinuidad. </li> 
      <li id="li_FED8686372DF4A39BAABC531BA4EB137">HLS Live no admite la sustitución de marcas de tiempo. </li> 
      <li id="li_565CFBEAD9874BA48F6E25B0893BF131">Los anuncios de la ventana DVR de las transmisiones en directo de HLS no se resuelven. </li> 
      <li id="li_7D22EA32C94240D79EDDA96D9E72FE8F">El rango de bytes no es compatible con contenido cifrado AES-128. </li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Contenido de DASH </td> 
   <td colname="col2"> <p>Recuerde lo siguiente: 
     <ul id="ul_9D33C2418F9F49DEAE0E642301726F89"> 
      <li id="li_74C69A21A7BD4831B92F0D57900E1CB1">Para emisiones en directo: se admite el perfil en directo con tipo dinámico. </li> 
      <li id="li_0C8743DB152047819D23C9F180998AD7">Para flujos de VOD: se admite el perfil activo con tipo estático. </li> 
      <li id="li_FBC6828663FB413798A4BDAF0B9831AA">Para flujos de VOD: el perfil bajo demanda no está certificado para flujos de trabajo de publicidad. </li> 
      <li id="li_4393B9B1F6144BDEAE484C879750ED23">No se admite la reproducción de secuencias de GUIÓN con varios períodos. </li> 
      <li id="li_6A2CEC4E974C4D44A45F5503A1A9D8D0">Se admiten subtítulos incrustados (608/708), indicados mediante la etiqueta Accesibilidad. </li> 
      <li id="li_EDE93DF4F3A64A53BA80877F701A8F0D">No se admiten archivos VTT fragmentados o segmentados. </li> 
      <li id="li_8897F73611194030A490A4FF1178364C">Los flujos con etiquetas personalizadas en banda no están certificados. </li> 
     </ul></p> </td> 
  </tr> 
 </tbody> 
</table>
