---
description: Cuando TVSDK detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar automáticamente la etiqueta y exponerla en forma de objeto PTTimedMetadata.
title: Clase de metadatos cronometrados
exl-id: b619b019-cb6d-4c31-a7e2-7ebe2f44a4b0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Clase de metadatos cronometrados{#timed-metadata-class}

Cuando TVSDK detecta una etiqueta suscrita en la lista de reproducción/manifiesto, el reproductor intenta procesar automáticamente la etiqueta y exponerla en forma de objeto PTTimedMetadata.

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
   <td colname="col1"> <span class="codeph"> metadataId</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span> </td> 
   <td colname="col2"> Identificador único de los metadatos sincronizados. Este valor generalmente se extrae del atributo de ID de señal/etiqueta. De lo contrario, se proporciona un valor aleatorio único. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> name</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span></td> 
   <td colname="col2"> Nombre de los metadatos cronometrados. Si el tipo es <span class="codeph"> ETIQUETA</span>, el valor representa el nombre de la señal/etiqueta. Si el tipo es <span class="codeph"> ID3</span>, es nulo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> hora</span> </td> 
   <td colname="col02"><span class="codeph"> CMTime</span></td> 
   <td colname="col2"> La posición de tiempo, en milisegundos, relativa al inicio del contenido principal donde estos metadatos cronometrados están presentes en el flujo. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> <span class="codeph"> PTTimedMetadataType</span></td> 
   <td colname="col2">El tipo de metadatos cronometrados. 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG: indica que los metadatos cronometrados se crearon a partir de una etiqueta en la lista de reproducción/manifiesto. </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - indica que los metadatos cronometrados se crearon a partir de una etiqueta ID3 en el flujo de medios. </li> 
    </ul> </td> 
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

* Si la extracción falla debido a un formato de etiqueta personalizado, la propiedad content siempre contiene los datos sin procesar de la etiqueta, que es la cadena después de los dos puntos. En este caso no se produce ningún error.

| Elemento | Descripción |
|---|---|
| TAG, ID3 | Tipos posibles de metadatos cronometrados. |
| `@property (nonatomic, assign) CMTime time` | La posición temporal, relativa al inicio del contenido principal, en la que estos metadatos se insertaron en el flujo. |
| `@property (nonatomic, assign) PTTimedMetadataType type` | Devuelve el tipo de metadatos cronometrados. |
| `@property (nonatomic, retain) NSString *metadataId` | Devuelve el ID extraído de los atributos de cue/etiqueta. De lo contrario, se proporciona un valor aleatorio único. |
| `@property (nonatomic, retain) NSString *name` | Devuelve el nombre de la señal, que suele ser el nombre de la etiqueta HLS. |
