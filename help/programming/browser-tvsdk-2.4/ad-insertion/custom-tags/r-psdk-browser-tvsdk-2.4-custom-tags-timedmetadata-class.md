---
description: Cuando el SDK del explorador detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar automáticamente la etiqueta y exponerla como un objeto TimedMetadata.
seo-description: Cuando el SDK del explorador detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar automáticamente la etiqueta y exponerla como un objeto TimedMetadata.
seo-title: Clase de metadatos temporizados
title: Clase de metadatos temporizados
uuid: 3f276618-5f61-4b41-bd2d-78e7f32178d9
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Clase de metadatos temporizados{#timed-metadata-class}

Cuando el SDK del explorador detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar automáticamente la etiqueta y exponerla como un objeto TimedMetadata.

La clase `TimedMetadata` proporciona los siguientes elementos:

<table id="table_5827A0626EDC45F68DC3E7644F3EFF69"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Propiedad </th> 
   <th colname="col02" class="entry"> Tipo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>type </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>Estos son los tipos de metadatos temporizados: 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">TAG: los metadatos temporizados se crearon a partir de una etiqueta de la lista de reproducción/manifiesto. </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3: los metadatos temporizados se crearon a partir de una etiqueta ID3 en el flujo de medios. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>time </p> </td> 
   <td colname="col02"> <p>Número </p> </td> 
   <td colname="col2"> <p>La posición de tiempo local (milisegundos) en relación con el inicio del contenido principal en el que están presentes los metadatos temporizados en el flujo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>Cadena </p> </td> 
   <td colname="col2"> <p>Identificador único de los metadatos temporizados. </p> <p>Normalmente se extrae del atributo de identificación de señal/etiqueta si está presente. De lo contrario, es un valor aleatorio único. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>name </p> </td> 
   <td colname="col02"> <p>Número </p> </td> 
   <td colname="col2"> <p>Nombre de los metadatos temporizados. </p> <p>Si el tipo es TAG, el valor representa el nombre del cue/etiqueta. Si el tipo es ID3, el valor es nulo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>content </p> </td> 
   <td colname="col02"> <p>Cadena </p> </td> 
   <td colname="col2"> <p>El contenido sin procesar de los metadatos temporizados. </p> <p>Si el tipo es TAG, el valor representa la lista completa del atributo de la etiqueta/cue. Si el tipo id3, el valor es nulo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>metadatos </p> </td> 
   <td colname="col02"> <p><span class="codeph"> Metadatos</span> </p> </td> 
   <td colname="col2"> <p>La información procesada/extraída de la etiqueta personalizada de lista de reproducción/manifiesto. </p> </td> 
  </tr> 
 </tbody> 
</table>

