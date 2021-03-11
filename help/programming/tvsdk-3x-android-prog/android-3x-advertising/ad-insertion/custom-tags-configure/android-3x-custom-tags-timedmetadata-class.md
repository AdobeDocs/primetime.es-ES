---
description: Cuando TVSDK detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar y exponer automáticamente la etiqueta en forma de objeto TimedMetadata .
title: Clase de metadatos temporizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Clase de metadatos temporizada {#timed-metadata-class}

Cuando TVSDK detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar y exponer automáticamente la etiqueta en forma de objeto TimedMetadata .

La clase proporciona los siguientes elementos:

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b> Propiedad </b></th> 
   <th colname="col02" class="entry"> <b> Tipo  </b></th> 
   <th colname="col2" class="entry"> <b> Descripción  </b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> id  </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>Identificador único de los metadatos temporizados. </p> <p>Normalmente, este valor se extrae del atributo cue/tag ID. De lo contrario, se proporciona un valor aleatorio único. Utilice <span class="codeph"> getId </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadata  </span> </td> 
   <td colname="col02"> Metadatos </td> 
   <td colname="col2"> <p>La información procesada/extraída de la etiqueta personalizada lista de reproducción/manifiesto. Utilice <span class="codeph"> getMetadata </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> Cadena </td> 
   <td colname="col2"> <p>Nombre de los metadatos temporizados. Si el tipo es <span class="codeph"> TAG </span>, el valor representa el nombre del cue/etiqueta. Si el tipo es <span class="codeph"> ID3 </span>, es nulo. Utilice <span class="codeph"> getName </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> time  </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>Posición temporal, en milisegundos, relativa al inicio del contenido principal en el que están presentes los metadatos temporizados en la emisión. Utilice <span class="codeph"> getTime </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type  </span> </td> 
   <td colname="col02"> Tipo </td> 
   <td colname="col2"> <p>Tipo de metadatos temporizados. Utilice <span class="codeph"> getType </span>. 
     <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
      <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG: indica que los metadatos temporizados se crearon a partir de una etiqueta de la lista de reproducción/manifiesto. </li> 
      <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 : indica que los metadatos temporizados se crearon a partir de una etiqueta ID3 en el flujo de medios. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

Recuerde lo siguiente:

* TVSDK extrae automáticamente la lista de atributos en pares clave-valor y almacena los atributos en la propiedad metadata.

   >[!TIP]
   >
   >Los datos complejos de las etiquetas personalizadas del manifiesto, como las cadenas con caracteres especiales, deben estar entre comillas. Por ejemplo:
   >
   >
   ```
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url= 
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* Si la extracción falla debido a un formato de etiqueta personalizado, la propiedad metadata estará vacía y la aplicación debe extraer la información real. En este caso, no se genera ningún error.

<table id="table_1BAE98BF23F641A3A5709EBE37B327F6"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Elemento  </b></th> 
   <th colname="col2" class="entry"> <b>Descripción</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> tipo de enumeración pública {TAG, ID3}  </span> </td> 
   <td colname="col2"> <p>Tipos posibles de metadatos temporizados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public TimedMetadata(Type type, long time, long id, String name, Metadata metadata);  </span> </td> 
   <td colname="col2"> <p>Constructor predeterminado (la hora es la hora de flujo local). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getTime();  </span> </td> 
   <td colname="col2"> <p>Posición temporal, relativa al inicio del contenido principal, donde estos metadatos se insertaron en el flujo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Metadata getMetadata();  </span> </td> 
   <td colname="col2"> <p>Los metadatos insertados en el flujo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Type getType();  </span> </td> 
   <td colname="col2"> <p>Devuelve el tipo de metadatos temporizados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getId();  </span> </td> 
   <td colname="col2"> <p>Devuelve el ID extraído de los atributos cue/tag. De lo contrario, se proporciona un valor aleatorio único. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public String getName();  </span> </td> 
   <td colname="col2"> <p>Devuelve el nombre del cue, que suele ser el nombre de la etiqueta HLS. </p> </td> 
  </tr> 
 </tbody> 
</table>