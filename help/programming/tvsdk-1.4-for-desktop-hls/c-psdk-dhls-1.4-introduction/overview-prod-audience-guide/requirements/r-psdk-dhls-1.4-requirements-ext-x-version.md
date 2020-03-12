---
description: 'La versión de #EXT-X-VERSION en el archivo .m3u8 afecta a las funciones disponibles para la aplicación y a las etiquetas EXT válidas en la lista de reproducción/manifiesto.'
seo-description: 'La versión de #EXT-X-VERSION en el archivo .m3u8 afecta a las funciones disponibles para la aplicación y a las etiquetas EXT válidas en la lista de reproducción/manifiesto.'
seo-title: '#EXT-X-VERSION requirements'
title: '#EXT-X-VERSION requirements'
uuid: c862df4a-88ba-4497-8b7c-b83fcb34b8bb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# #EXT-X-VERSION requirements{#ext-x-version-requirements}

La versión de #EXT-X-VERSION en el archivo .m3u8 afecta a las funciones disponibles para la aplicación y a las etiquetas EXT válidas en la lista de reproducción/manifiesto.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

A continuación se proporciona información sobre la `#EXT-X-VERSION` etiqueta, que especifica la versión del protocolo HLS:

* La versión debe coincidir con las características y atributos de la lista de reproducción de HLS; de lo contrario, podrían producirse errores de reproducción.

   Para obtener más información, consulte la especificación [](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)HTTP Live Streaming.
* La versión debe coincidir con las características y atributos de la lista de reproducción de HLS; de lo contrario, podrían producirse errores de reproducción.

   Para obtener más información, consulte la especificación [](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)HTTP Live Streaming.
* Adobe recomienda utilizar al menos la versión 2 para la reproducción en clientes basados en.

   Los clientes y los servidores deben implementar las versiones de la siguiente manera:

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
   <td colname="2"> Atributo IV de la <span class="codeph"> etiqueta EXT-X-KEY </span> . </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duración <span class="codeph"> EXTINF de punto flotante </span> <p>Las etiquetas de duración ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) en la versión 2 se redondearon a valores enteros. La versión 3 y posteriores requieren duraciones exactas en el punto flotante. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6">La <span class="codeph"> etiqueta EXT-X-BYTERANGE </span> </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6">La <span class="codeph"> etiqueta EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD">La <span class="codeph"> etiqueta EXT-X-I-FRAMES SOLO </span> </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB">La <span class="codeph"> etiqueta EXT-X-MEDIA </span> </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">Los <span class="codeph"> atributos AUDIO </span> y <span class="codeph"> VIDEO </span> de la etiqueta <span class="codeph"> EXT-X-STREAM-INF </span> </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">Audio alternativo TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

