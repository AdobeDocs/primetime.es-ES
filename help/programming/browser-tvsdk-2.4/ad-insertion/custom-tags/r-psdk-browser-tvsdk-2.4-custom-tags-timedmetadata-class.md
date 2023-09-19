---
description: Cuando el TVSDK del explorador detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar automáticamente la etiqueta y exponerla como un objeto TimedMetadata.
title: Clase de metadatos cronometrados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Clase de metadatos cronometrados{#timed-metadata-class}

Cuando el TVSDK del explorador detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar automáticamente la etiqueta y exponerla como un objeto TimedMetadata.

El `TimedMetadata` proporciona los siguientes elementos:

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
   <td colname="col2"> <p>Estos son los tipos de metadatos cronometrados: 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">ETIQUETA: los metadatos cronometrados se crearon a partir de una etiqueta en la lista de reproducción/manifiesto. </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3: los metadatos cronometrados se crearon a partir de una etiqueta ID3 en el flujo de medios. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>hora </p> </td> 
   <td colname="col02"> <p>Número </p> </td> 
   <td colname="col2"> <p>La posición de la hora local (milisegundos) en relación con el inicio del contenido principal donde estos metadatos cronometrados están presentes en el flujo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>Cadena </p> </td> 
   <td colname="col2"> <p>El identificador único de los metadatos cronometrados. </p> <p>Normalmente se extrae del atributo de ID de señal/etiqueta, si lo hay. De lo contrario, es un valor aleatorio único. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>name </p> </td> 
   <td colname="col02"> <p>Número </p> </td> 
   <td colname="col2"> <p>Nombre de los metadatos cronometrados. </p> <p>Si el tipo es TAG, el valor representa el nombre de la señal/etiqueta. Si el tipo es ID3, el valor es nulo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>content </p> </td> 
   <td colname="col02"> <p>Cadena </p> </td> 
   <td colname="col2"> <p>El contenido sin procesar de los metadatos cronometrados. </p> <p>Si el tipo es TAG, el valor representa toda la lista de atributos de la señal/etiqueta. Si el tipo es ID3, el valor es nulo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>metadatos </p> </td> 
   <td colname="col02"> <p><span class="codeph"> Metadatos</span> </p> </td> 
   <td colname="col2"> <p>La información procesada/extraída de la etiqueta personalizada de lista de reproducción/manifiesto. </p> </td> 
  </tr> 
 </tbody> 
</table>
