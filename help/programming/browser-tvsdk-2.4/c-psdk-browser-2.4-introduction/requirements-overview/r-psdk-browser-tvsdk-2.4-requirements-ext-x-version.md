---
description: La versión de `#`EXT-X-VERSION en el archivo .m3u8 afecta a las funciones disponibles para la aplicación y a las etiquetas EXT válidas en la lista de reproducción/manifiesto.
title: '`#`EXT-X-VERSION'
exl-id: 1b7c205b-c6b1-416f-885a-d1cd23d8e803
source-git-commit: 8610792a7410dab59d42ab7771b534c2c1670ad2
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `#`Requisitos de EXT-X-VERSION{#ext-x-version-requirements}

La versión de #EXT-X-VERSION en el archivo .m3u8 afecta a las características disponibles para su aplicación y a las etiquetas EXT válidas en su lista de reproducción/manifiesto.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

Aquí puede encontrar más información sobre la etiqueta `#EXT-X-VERSION` , que especifica la versión del protocolo HLS:

* La versión debe coincidir con las funciones y atributos de la lista de reproducción de HLS; de lo contrario, podrían producirse errores de reproducción. Para obtener más información, consulte [Especificación de transmisión en directo HTTP](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Adobe recomienda utilizar al menos la versión 2 para la reproducción en clientes basados en TVSDK del explorador.

   Los clientes y servidores deben implementar las versiones de la siguiente manera:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Usar al menos esta versión </th> 
   <th colname="2" class="entry"> Para usar estas funciones </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duración <span class="codeph"> EXTINF </span> de punto flotante <p>Las etiquetas de duración ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) en la versión 2 se redondearon a valores enteros. La versión 3 y superiores requieren duraciones exactas en coma flotante. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4  </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">La etiqueta <span class="codeph"> EXT-X-MEDIA </span> </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">Los atributos <span class="codeph"> AUDIO </span> y <span class="codeph"> VIDEO </span> de la etiqueta <span class="codeph"> EXT-X-STREAM-INF </span> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
