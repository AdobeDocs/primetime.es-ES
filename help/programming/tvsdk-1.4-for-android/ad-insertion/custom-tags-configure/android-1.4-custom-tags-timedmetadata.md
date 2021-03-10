---
description: Cuando TVSDK detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta automáticamente procesar la etiqueta y exponerla en forma de objeto TimedMetadata .
title: Clase de metadatos temporizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---


# Clase de metadatos temporizada{#timed-metadata-class}

Cuando TVSDK detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta automáticamente procesar la etiqueta y exponerla en forma de objeto TimedMetadata .

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
   <td colname="col1"> <span class="codeph"> id  </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> Identificador único de los metadatos temporizados. Normalmente, este valor se extrae del atributo cue/tag ID. De lo contrario, se proporciona un valor aleatorio único. Utilice <span class="codeph"> getId </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadata  </span> </td> 
   <td colname="col02"> Metadatos </td> 
   <td colname="col2"> La información procesada/extraída de la etiqueta personalizada lista de reproducción/manifiesto. Utilice <span class="codeph"> getMetadata </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> Cadena </td> 
   <td colname="col2"> Nombre de los metadatos temporizados. Si el tipo es <span class="codeph"> TAG </span>, el valor representa el nombre del cue/etiqueta. Si el tipo es <span class="codeph"> ID3 </span>, es nulo. Utilice <span class="codeph"> getName </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> time  </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> Posición temporal, en milisegundos, relativa al inicio del contenido principal en el que están presentes los metadatos temporizados en la emisión. Utilice <span class="codeph"> getTime </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type  </span> </td> 
   <td colname="col02"> Tipo </td> 
   <td colname="col2"> Tipo de metadatos temporizados. Utilice <span class="codeph"> getType </span>. 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG: indica que los metadatos temporizados se crearon a partir de una etiqueta de la lista de reproducción/manifiesto. </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 : indica que los metadatos temporizados se crearon a partir de una etiqueta ID3 en el flujo de medios. </li> 
    </ul> </td> 
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
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0, 
   >url="www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* Si la extracción falla debido a un formato de etiqueta personalizado, la propiedad metadata estará vacía y la aplicación debe extraer la información real. En este caso no se genera ningún error.

| Elemento | Descripción |
|---|---|
| `public enum Type { TAG, ID3}` | Tipos posibles de metadatos temporizados. |
| `public TimedMetadata(Type type, long time, long id, String name, Metadata metadata);` | Constructor predeterminado (la hora es la hora de flujo local). |
| `public long getTime();` | Posición temporal, relativa al inicio del contenido principal, donde estos metadatos se insertaron en el flujo. |
| `public Metadata getMetadata();` | Los metadatos insertados en el flujo. |
| `public Type getType();` | Devuelve el tipo de metadatos temporizados. |
| `public long getId();` | Devuelve el ID extraído de los atributos cue/tag. De lo contrario, se proporciona un valor aleatorio único. |
| `public String getName();` | Devuelve el nombre del cue, que suele ser el nombre de la etiqueta HLS. |

