---
description: Actualmente, TVSDK proporciona compatibilidad integrada con metadatos del proveedor de publicidad para anuncios TVSDK, saltos de publicidad directos y marcadores de publicidad personalizados.
seo-description: Actualmente, TVSDK proporciona compatibilidad integrada con metadatos del proveedor de publicidad para anuncios TVSDK, saltos de publicidad directos y marcadores de publicidad personalizados.
seo-title: Tipos de inserción de publicidad
title: Tipos de inserción de publicidad
uuid: 6b5c3555-1ddd-4215-8bb2-03d16bb818c5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Tipos de inserción de publicidad {#ad-insertion-types}

Actualmente, TVSDK proporciona compatibilidad integrada con metadatos del proveedor de publicidad para anuncios TVSDK, saltos de publicidad directos y marcadores de publicidad personalizados.

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
   <td colname="col1"> Publicidades de Adobe Primetime y decisiones </td> 
   <td colname="col2">VOD <p>Live Live </p> <p>Lineal </p> </td> 
   <td colname="col3">La implementación de referencia proporciona <span class="codeph"> información de AuditudeMetadata</span> para conectarse al servidor para la toma de decisiones y Primetime (anteriormente conocido como Auditude), en función de la información proporcionada en la porción</a> de anuncios Primetime del archivo</a>de configuración JSON. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Saltos publicitarios directos </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Debe proporcionar direcciones URL de publicidad en el archivo JSON de entrada. Cuando TVSDK intenta resolver una publicidad, llama a la resolución directa de errores de publicidad y resuelve las publicidades en función de la información de saltos de publicidad directa proporcionada en el archivo</a>de configuración JSON. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marcadores de publicidad personalizados </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Los marcadores de publicidad personalizados son útiles cuando el flujo de vídeo contiene tanto contenido principal como anuncios, pero no incluye información relacionada con las posiciones y la temporización de los anuncios. Si la información de posición de publicidad se obtiene de otra manera, por ejemplo, a través de un CMS externo, puede definir marcadores de publicidad personalizados y pasarlos a la línea de tiempo del reproductor. <p>Para configurar un reproductor para la inserción de publicidad, debe pasar los metadatos de publicidad en la sección de metadatos de publicidad personalizados del archivo</a>de configuración JSON, que tiene una implementación de proveedor de publicidad compatible en la implementación de referencia. </p> </td>
  </tr>
 </tbody>
</table>