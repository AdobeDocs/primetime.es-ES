---
description: Cuando TVSDK detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar automáticamente la etiqueta y exponerla en forma de objeto TimedMetadata.
seo-description: Cuando TVSDK detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar automáticamente la etiqueta y exponerla en forma de objeto TimedMetadata.
seo-title: Clase de metadatos temporizados
title: Clase de metadatos temporizados
uuid: 827a3bcf-a584-4032-aa19-4fc7730778cc
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Clase de metadatos temporizados{#timed-metadata-class}

Cuando TVSDK detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar automáticamente la etiqueta y exponerla en forma de objeto TimedMetadata.

La clase proporciona los siguientes elementos:

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Propiedad </th> 
   <th colname="col02" class="entry"> Tipo </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> content</span> </td> 
   <td colname="col02"> Cadena </td> 
   <td colname="col2"> El contenido sin procesar de los metadatos temporizados. Si el tipo es TAG, el valor representa la lista completa de atributos de la etiqueta/cue. Si el tipo id3, es nulo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> id</span> </td> 
   <td colname="col02"> Cadena </td> 
   <td colname="col2"> Identificador único de los metadatos temporizados. Normalmente, este valor se extrae del atributo cue/tag ID. De lo contrario, se proporciona un valor aleatorio único. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> metadatos</span> </td> 
   <td colname="col02"> Metadatos </td> 
   <td colname="col2"> La información procesada/extraída de la etiqueta personalizada de lista de reproducción/manifiesto. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> name</span> </td> 
   <td colname="col02"> Cadena </td> 
   <td colname="col2">Nombre de los metadatos temporizados. Si el tipo es <span class="codeph"> TAG</span>, el valor representa el nombre del cue/etiqueta. Si el tipo es <span class="codeph"> ID3</span>, es nulo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> time</span> </td> 
   <td colname="col02"> Número </td> 
   <td colname="col2"> La posición de tiempo, en milisegundos, en relación con el inicio del contenido principal en el que están presentes los metadatos temporizados en el flujo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> Cadena </td> 
   <td colname="col2">Tipo de metadatos temporizados. 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG: indica que los metadatos temporizados se crearon a partir de una etiqueta de la lista de reproducción/manifiesto. </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3: indica que los metadatos temporizados se crearon a partir de una etiqueta ID3 en el flujo de medios. </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

Recuerde lo siguiente:

* TVSDK extrae automáticamente la lista de atributos en pares clave-valor y almacena los atributos en la propiedad metadata.

   >[!TIP]
   >
   >Los datos complejos de las etiquetas personalizadas del manifiesto, como las cadenas con caracteres especiales, deben estar entre comillas. Por ejemplo:   >
   >
   >
   ```>
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url=
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```  >
   >



* Si la extracción falla debido a un formato de etiqueta personalizado, la propiedad metadata estará vacía y la aplicación debe extraer la información real. En este caso no se genera ningún error.

| Elemento | Descripción |
|---|---|
| `TAG, ID3 ID3, TAG` | Tipos posibles para los metadatos temporizados. |
| `public function TimedMetadata(type:String, time:Number, id:String, name:String, content:String, metadata:Metadata)` | Constructor predeterminado (tiempo es el tiempo de flujo local). |
| `content:String` | El contenido sin procesar de la etiqueta de origen de estos metadatos temporizados. |
| `time:Number` | La posición de tiempo, en relación con el inicio del contenido principal, donde se insertaron estos metadatos en el flujo. |
| `metadata:Metadata` | Metadatos insertados en el flujo. |
| `type:String` | Devuelve el tipo de metadatos temporizados. |
| `id:String` | Devuelve el ID extraído de los atributos cue/tag. De lo contrario, se proporciona un valor aleatorio único. |
| `name:String` | Devuelve el nombre del cue, que suele ser el nombre de la etiqueta HLS. |

