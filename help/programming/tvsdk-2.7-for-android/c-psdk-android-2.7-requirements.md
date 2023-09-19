---
description: TVSDK tiene requisitos específicos para el contenido multimedia, el contenido de manifiesto, DRM y las versiones de software.
title: Requisitos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Requisitos {#requirements}

TVSDK tiene requisitos específicos para el contenido multimedia, el contenido de manifiesto, DRM y las versiones de software.

## Requisitos de sistema y software {#section_96E5B079900246E78682AE44D3F23068}

Para utilizar TVSDK, asegúrese de que las versiones de hardware, sistema operativo y aplicación cumplan todos los requisitos mínimos que se indican a continuación.

| Sistema operativo | Android 4.0 o posterior (nivel mínimo de API 14) |
|---|---|
| CPU | Un núcleo de 1 GHz o equivalente |
| RAM | 256 MB |
| GPU | GPU de hardware necesaria para la reproducción |
| Arquitectura | x86 mediante Houdini, ARM64, ARMv7 y ARMv8 |

## Requisitos de contenido y manifiesto {#section_72DD0E4DA9774DCCADB42887497F1386}

Compruebe las restricciones y requisitos para emisiones y listas de reproducción (manifiestos), incluidas las claves de cifrado DRM.

| DRM de acceso a Adobe | Si el flujo protegido por DRM tiene una velocidad de bits múltiple (MBR), la clave de cifrado DRM utilizada para el MBR debe ser la misma que la utilizada en todos los flujos de velocidad de bits. |
|---|---|
| Manifiestos de variante de anuncio | Must have the same bit-rate renditions as the renditions of the main content. |

## #EXT-X-VERSION requisitos {#section_49A33664651A46EC9ED888BA9C1C3F6D}

La versión de `#EXT-X-VERSION` en el archivo de manifiesto [!DNL .m3u8] afecta a las características disponibles para la aplicación y a las etiquetas `EXT` que son válidas.

A continuación se proporciona información sobre la etiqueta `#EXT-X-VERSION`, que especifica la versión del protocolo HLS:

* La versión debe coincidir con las funciones y atributos de la lista de reproducción de HLS; de lo contrario, podrían producirse errores de reproducción. Para obtener más información, consulte [Especificación de flujo en directo HTTP](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Adobe recomienda utilizar al menos la versión 2 de HLS para la reproducción en clientes basados en TVSDK.

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
   <td colname="2"> El atributo IV del <span class="codeph"> EXT-X-KEY </span> etiqueta. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duración de punto flotante <span class="codeph"> EXTINF </span> <p>Las etiquetas de duración ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) en la versión 2 se redondearon a valores enteros. La versión 3 y posteriores requieren que las duraciones se especifiquen exactamente, en coma flotante. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">El <span class="codeph"> EXT-X-BYTERANGE </span> etiqueta </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">El <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> etiqueta </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">El <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> etiqueta </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">El <span class="codeph"> EXT-X-MEDIA </span> etiqueta </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">El <span class="codeph"> AUDIO </span> y <span class="codeph"> VÍDEO </span> atributos del <span class="codeph"> EXT-X-STREAM-INF </span> etiqueta </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">Audio alternativo de TVSDK </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
