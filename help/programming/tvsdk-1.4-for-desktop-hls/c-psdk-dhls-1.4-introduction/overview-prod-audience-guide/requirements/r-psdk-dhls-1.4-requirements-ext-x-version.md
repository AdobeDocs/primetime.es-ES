---
description: La versión de EXT-X-VERSION en el archivo .m3u8 afecta a las funciones disponibles para su aplicación y a las etiquetas EXT válidas en la lista de reproducción/manifiesto.
title: REQUISITOS DE LA VERSIÓN EXT-X
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# REQUISITOS DE LA VERSIÓN EXT-X{#ext-x-version-requirements}

La versión de #EXT-X-VERSION en el archivo .m3u8 afecta a las funciones disponibles para su aplicación y a las etiquetas EXT válidas en la lista de reproducción/manifiesto.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

A continuación se proporciona información sobre la etiqueta `#EXT-X-VERSION`, que especifica la versión del protocolo HLS:

* La versión debe coincidir con las funciones y atributos de la lista de reproducción de HLS; de lo contrario, podrían producirse errores de reproducción.

  Para obtener más información, consulte [Especificación de flujo en directo HTTP](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* La versión debe coincidir con las funciones y atributos de la lista de reproducción de HLS; de lo contrario, podrían producirse errores de reproducción.

  Para obtener más información, consulte [Especificación de flujo en directo HTTP](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Adobe recomienda utilizar al menos la versión 2 para la reproducción en clientes basados en.

  Los clientes y servidores deben implementar las versiones de la siguiente manera:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Usar al menos esta versión </th> 
   <th colname="2" class="entry"> Para utilizar estas funciones </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> Atributo IV de la etiqueta <span class="codeph"> EXT-X-KEY </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duración de punto flotante <span class="codeph"> EXTINF </span> <p>Las etiquetas de duración ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) en la versión 2 se redondearon a valores enteros. La versión 3 y posteriores requieren que las duraciones sean exactas en coma flotante. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6">La etiqueta <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6">La etiqueta <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD">La etiqueta <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB">La etiqueta <span class="codeph"> EXT-X-MEDIA </span> </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">El <span class="codeph"> AUDIO </span> y <span class="codeph"> VÍDEO </span> atributos del <span class="codeph"> EXT-X-STREAM-INF </span> etiqueta </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">Audio alternativo de TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
