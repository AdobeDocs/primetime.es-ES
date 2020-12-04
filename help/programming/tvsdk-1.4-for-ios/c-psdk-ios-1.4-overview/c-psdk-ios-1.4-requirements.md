---
description: TVSDK requiere propiedades específicas para el contenido multimedia, el contenido de manifiesto y las versiones de software.
seo-description: TVSDK requiere propiedades específicas para el contenido multimedia, el contenido de manifiesto y las versiones de software.
seo-title: Requisitos
title: Requisitos
uuid: 7e5fb176-4c3f-4c12-9080-3afced28627b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Requisitos {#requirements}

TVSDK requiere propiedades específicas para el contenido multimedia, el contenido de manifiesto y las versiones de software.

## Requisitos del sistema y del software {#section_61C32A0209C44230B392B113B85643EE}

Para utilizar TVSDK, asegúrese de que todas las versiones de hardware, sistema operativo y aplicación cumplen los requisitos mínimos que se indican a continuación.

Sistema operativo: iOS 6.0 o posterior

## Requisitos de contenido y manifiesto {#section_05FA02E2189742008DA09D87E66DCAB7}

Compruebe las restricciones y los requisitos de los flujos y listas de reproducción (manifiestos), incluidas las claves de cifrado DRM.

| Marcos clave del segmento de contenido | Cada segmento de contenido debe comenzar con un marco clave. |
|---|---|
| Números de secuencia en vídeo en directo/lineal | Debe coincidir con todas las representaciones de velocidad de bits del contenido principal en cualquier momento. |

## #EXT-X-VERSION requirements {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

La versión de `#EXT-X-VERSION` en el archivo [!DNL .m3u8] afecta a las características disponibles para la aplicación y a las etiquetas `EXT` válidas en la lista de reproducción/manifiesto.

A continuación encontrará información sobre la etiqueta `#EXT-X-VERSION`, que especifica la versión del protocolo HLS:

* La versión debe coincidir con las características y atributos de la lista de reproducción de HLS; de lo contrario, podrían producirse errores de reproducción.

   Para obtener más información, consulte la [especificación HTTP Live Streaming](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Si la etiqueta no está incluida en las listas de reproducción de medios o maestros, o si no se especifica ninguna versión, se utiliza la versión 1 de forma predeterminada. El contenido que no cumpla con la versión 1 no se reproducirá.
* Adobe recomienda utilizar al menos la versión 2 para la reproducción en clientes basados en TVSDK.

Los clientes y los servidores deben implementar las versiones de la siguiente manera:

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> Usar al menos esta versión </th> 
   <th colname="2" class="entry"> Para utilizar estas funciones </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2  </span> </td> 
   <td colname="2"> El atributo IV de la etiqueta <span class="codeph"> EXT-X-KEY </span>. </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valores de duración del punto flotante <span class="codeph"> EXTINF </span> <p>Las etiquetas de duración ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) en la versión 2 se redondearon a valores enteros. La versión 3 y posteriores requieren duraciones exactas en el punto flotante. </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> Funciones de TVSDK como inserción de anuncios y ABR transparente </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4  </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927">La etiqueta <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF">La etiqueta <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">La etiqueta <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">La etiqueta <span class="codeph"> EXT-X-MEDIA </span> </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">Los atributos <span class="codeph"> AUDIO </span> y <span class="codeph"> VIDEO </span> de la etiqueta <span class="codeph"> EXT-X-STREAM-INF </span> </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> Audio alternativo TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
