---
description: Actualmente, TVSDK proporciona compatibilidad con metadatos de proveedor de publicidad integrada para anuncios TVSDK, pausas publicitarias directas y marcadores de publicidad personalizados.
title: Tipos de inserción de publicidad
exl-id: 1634ff41-8a8f-4f34-9685-149ec58518ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Tipos de inserción de publicidad {#ad-insertion-types}

Actualmente, TVSDK proporciona compatibilidad con metadatos de proveedor de publicidad integrada para anuncios TVSDK, pausas publicitarias directas y marcadores de publicidad personalizados.

Admite los siguientes tipos de flujos de trabajo de inserción de publicidad para contenido de VOD y contenido en directo/lineal.

<table id="table_1C3A659BDDB7453CA953A103045FCA01"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Tipo de inserción </th> 
   <th colname="col2" class="entry"> Compatible con... </th> 
   <th colname="col3" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Anuncios de Adobe Primetime ad decisioning </td> 
   <td colname="col2">VOD <p>Activo </p> <p>Lineal </p> </td> 
   <td colname="col3">La implementación de referencia proporciona lo siguiente <span class="codeph"> AuditudeMetadata</span> información para conectarse al servidor de para la toma de decisiones de anuncios de Primetime (anteriormente conocida como Auditude), en función de la información proporcionada en la sección de anuncios de Primetime</a> del archivo de configuración JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Saltos de publicidad directos </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Debe proporcionar direcciones URL de publicidad en el archivo JSON de entrada. Cuando TVSDK intenta resolver un anuncio, llama a la resolución de pausas publicitarias directas y resuelve los anuncios en función de la información de pausas publicitarias directas proporcionada en el archivo de configuración JSON</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marcadores de publicidad personalizados </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3">Los marcadores de publicidad personalizados son útiles cuando el flujo de vídeo contiene contenido principal y anuncios, pero no incluyen información relacionada con las posiciones y el tiempo de los anuncios. Si la información de colocación de la publicidad se obtiene de otra manera, por ejemplo, a través de un CMS externo, puede definir marcadores de publicidad personalizados y pasarlos a la cronología del reproductor. <p>Para configurar un reproductor para la inserción de anuncios, debe pasar metadatos de publicidad en la sección de metadatos de publicidad personalizados del archivo de configuración JSON</a>, que tiene una implementación de proveedor de publicidad de soporte en la implementación de referencia. </p> </td>
  </tr>
 </tbody>
</table>
