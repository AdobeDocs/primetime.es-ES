---
description: Actualmente, TVSDK proporciona compatibilidad integrada con metadatos del proveedor de publicidad para anuncios TVSDK, pausas publicitarias directas y marcadores de anuncios personalizados.
title: Tipos de inserción de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Tipos de inserción de publicidad {#ad-insertion-types}

Actualmente, TVSDK proporciona compatibilidad integrada con metadatos del proveedor de publicidad para anuncios TVSDK, pausas publicitarias directas y marcadores de anuncios personalizados.

Admite los siguientes tipos de flujos de trabajo de inserción de anuncios para VOD y contenido en directo/lineal.

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Tipo de inserción </th> 
   <th colname="col2" class="entry"> Admitido en... </th> 
   <th colname="col3" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Anuncios de Adobe Primetime Ad Decisioning </td> 
   <td colname="col2">VOD <p>Activo </p> <p>Lineal </p> </td> 
   <td colname="col3">La implementación de referencia proporciona información de <span class="codeph"> AuditudeMetadata</span> para conectarse al servidor para la toma de decisiones de anuncios de Primetime (anteriormente conocido como Auditude), basada en la información proporcionada en la parte de anuncios de Primetime</a> del archivo de configuración JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Pausas publicitarias directas </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Debe proporcionar direcciones URL de publicidad en el archivo JSON de entrada. Cuando el TVSDK intenta resolver un anuncio, llama a la resolución directa de las pausas publicitarias y resuelve los anuncios en función de las pausas publicitarias directas que se proporcionan en el archivo de configuración JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marcadores de anuncio personalizados </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Los marcadores de publicidad personalizados son útiles cuando el flujo de vídeo contiene tanto contenido principal como anuncios, pero no incluyen información relacionada con las posiciones y la temporización de los anuncios. Si la información de posicionamiento de la publicidad se obtiene de otra manera, por ejemplo, a través de un CMS externo, puede definir marcadores de anuncios personalizados y pasarlos a la cronología del reproductor. <p>Para configurar un reproductor para la inserción de publicidad, debe pasar los metadatos de publicidad en la sección de metadatos de publicidad personalizados del archivo de configuración JSON</a>, que tiene una implementación de proveedor de publicidad compatible en la implementación de referencia. </p> </td>
  </tr>
 </tbody>
</table>