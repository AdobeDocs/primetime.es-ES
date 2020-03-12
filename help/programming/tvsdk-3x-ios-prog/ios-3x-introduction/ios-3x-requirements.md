---
description: TVSDK tiene requisitos específicos para contenido multimedia, contenido de manifiesto, DRM y versiones de software.
seo-description: TVSDK tiene requisitos específicos para contenido multimedia, contenido de manifiesto, DRM y versiones de software.
seo-title: Requisitos
title: Requisitos
uuid: 06e61b9f-cda2-4813-8da4-fb3e0d88ad35
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Requisitos {#requirements}

TVSDK requiere propiedades específicas para contenido multimedia, contenido de manifiesto, DRM y versiones de software.

## Requisitos de sistema y software {#section_96E5B079900246E78682AE44D3F23068}

Para utilizar TVSDK, asegúrese de que todas las versiones de hardware, sistema operativo y aplicación cumplen los requisitos mínimos que se indican a continuación.

| Sistema operativo | iOS 7.0 o posterior |
|---|---|
| Xcode | Xcode 10 para iOS 12 y Xcode 9 para iOS 11 |

## Requisitos de contenido y manifiesto {#section_72DD0E4DA9774DCCADB42887497F1386}

Compruebe las restricciones y los requisitos de los flujos y listas de reproducción (manifiestos), incluidas las claves de cifrado DRM.

| Marcos clave del segmento de contenido | Cada segmento de contenido debe comenzar con un marco clave. |
|---|---|
| Números de secuencia en vídeo en directo/lineal | Debe coincidir con todas las representaciones de velocidad de bits del contenido principal en cualquier momento. |

## Requisitos de EXT-X-VERSION {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

La versión de `#EXT-X-VERSION` en el archivo de [!DNL .m3u8] manifiesto afecta a las funciones disponibles para la aplicación y a `EXT` las etiquetas válidas.

A continuación se proporciona información sobre la `#EXT-X-VERSION` etiqueta, que especifica la versión del protocolo HLS:

* La versión debe coincidir con las características y atributos de la lista de reproducción de HLS; de lo contrario, podrían producirse errores de reproducción. Para obtener más información, consulte la especificación [](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)HTTP Live Streaming.
* Adobe recomienda utilizar al menos la versión 2 de HLS para la reproducción en clientes basados en TVSDK.

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
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duración <span class="codeph"> EXTINF de punto flotante </span> <p>Las etiquetas de duración ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) en la versión 2 se redondearon a valores enteros. La versión 3 y posteriores requieren que las duraciones se especifiquen exactamente, en coma flotante. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">La <span class="codeph"> etiqueta EXT-X-BYTERANGE </span> </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">La <span class="codeph"> etiqueta EXT-X-I-FRAME-STREAM-INF </span> </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">La <span class="codeph"> etiqueta EXT-X-I-FRAMES SOLO </span> </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">La <span class="codeph"> etiqueta EXT-X-MEDIA </span> </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">Los <span class="codeph"> atributos AUDIO </span> y <span class="codeph"> VIDEO </span> de la etiqueta <span class="codeph"> EXT-X-STREAM-INF </span> </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">Audio alternativo TVSDK </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>