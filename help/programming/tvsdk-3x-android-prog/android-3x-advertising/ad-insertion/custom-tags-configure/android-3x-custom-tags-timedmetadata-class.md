---
description: Cuando TVSDK detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar y exponer automáticamente la etiqueta en forma de objeto TimedMetadata.
title: Clase de metadatos cronometrados
exl-id: abb552d0-42f9-495e-a307-1f03d6a0b965
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Clase de metadatos cronometrados {#timed-metadata-class}

Cuando TVSDK detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar y exponer automáticamente la etiqueta en forma de objeto TimedMetadata.

La clase proporciona los siguientes elementos:

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b> Propiedad </b></th> 
   <th colname="col02" class="entry"> <b> Tipo </b></th> 
   <th colname="col2" class="entry"> <b> Descripción </b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> largo </td> 
   <td colname="col2"> <p>Identificador único de los metadatos sincronizados. </p> <p>Este valor generalmente se extrae del atributo de ID de señal/etiqueta. De lo contrario, se proporciona un valor aleatorio único. Uso <span class="codeph"> getId </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadatos </span> </td> 
   <td colname="col02"> Metadatos </td> 
   <td colname="col2"> <p>La información procesada/extraída de la etiqueta personalizada de lista de reproducción/manifiesto. Uso <span class="codeph"> getMetadata </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> Cadena </td> 
   <td colname="col2"> <p>Nombre de los metadatos cronometrados. Si el tipo es <span class="codeph"> ETIQUETA </span>, el valor representa el nombre de la señal/etiqueta. Si el tipo es <span class="codeph"> ID3 </span>, es nulo. Uso <span class="codeph"> getName </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> hora </span> </td> 
   <td colname="col02"> largo </td> 
   <td colname="col2"> <p>La posición de tiempo, en milisegundos, relativa al inicio del contenido principal donde estos metadatos cronometrados están presentes en el flujo. Uso <span class="codeph"> getTime </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type </span> </td> 
   <td colname="col02"> Tipo </td> 
   <td colname="col2"> <p>El tipo de metadatos cronometrados. Uso <span class="codeph"> getType </span>. 
     <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
      <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG: indica que los metadatos cronometrados se crearon a partir de una etiqueta en la lista de reproducción/manifiesto. </li> 
      <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - indica que los metadatos cronometrados se crearon a partir de una etiqueta ID3 en el flujo de medios. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

Recuerde lo siguiente:

* TVSDK extrae automáticamente la lista de atributos en pares clave-valor y almacena los atributos en la propiedad de metadatos.

   >[!TIP]
   >
   >Los datos complejos de las etiquetas personalizadas del manifiesto, como cadenas con caracteres especiales, deben estar entre comillas. Por ejemplo:
   >
   >
   ```
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url= 
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* Si la extracción falla debido a un formato de etiqueta personalizado, la propiedad de metadatos estará vacía y la aplicación debe extraer la información real. En este caso, no se produce ningún error.

<table id="table_1BAE98BF23F641A3A5709EBE37B327F6"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Elemento </b></th> 
   <th colname="col2" class="entry"> <b>Descripción</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Tipo de enumeración pública {TAG, ID3} </span> </td> 
   <td colname="col2"> <p>Tipos posibles de metadatos cronometrados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public TimedMetadata(Type type, long time, long id, String name, Metadata metadata); </span> </td> 
   <td colname="col2"> <p>Constructor predeterminado (la hora es la hora de la secuencia local). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getTime(); </span> </td> 
   <td colname="col2"> <p>La posición temporal, relativa al inicio del contenido principal, en la que estos metadatos se insertaron en el flujo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Metadata getMetadata(); </span> </td> 
   <td colname="col2"> <p>Los metadatos insertados en el flujo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Type getType(); </span> </td> 
   <td colname="col2"> <p>Devuelve el tipo de metadatos cronometrados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getId(); </span> </td> 
   <td colname="col2"> <p>Devuelve el ID extraído de los atributos de cue/etiqueta. De lo contrario, se proporciona un valor aleatorio único. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public String getName(); </span> </td> 
   <td colname="col2"> <p>Devuelve el nombre de la señal, que suele ser el nombre de la etiqueta HLS. </p> </td> 
  </tr> 
 </tbody> 
</table>
