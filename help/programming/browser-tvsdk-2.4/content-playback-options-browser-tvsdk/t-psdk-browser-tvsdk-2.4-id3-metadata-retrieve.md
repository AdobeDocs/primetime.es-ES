---
description: Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. TVSDK del explorador detecta las etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y envía un evento. La aplicación puede extraer datos de la etiqueta.
title: Etiquetas ID3
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Etiquetas ID3{#id-tags}

Las etiquetas ID3 proporcionan información sobre un archivo de audio o vídeo, como el título del archivo o el nombre del artista. TVSDK del explorador detecta las etiquetas ID3 en el nivel de segmento de flujo de transporte (TS) en flujos HLS y envía un evento. La aplicación puede extraer datos de la etiqueta.

Cuando se encuentra un nuevo metadato ID3 en el flujo HLS subyacente, el explorador TVSDK déclencheur un `AdobePSDK.TimedMetadataEvent` evento.

El `TimedMetadata` para ID3 tiene las siguientes propiedades:

<table id="table_6C61886187FB44B4B9821E4B00200018"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Nombre de propiedad </th> 
   <th colname="col2" class="entry"> Detalles </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> type </span> </p> </td> 
   <td colname="col2"> <p>Un tipo de <span class="codeph"> TimedMetadata </span> objeto. </p> <p>Para los metadatos de ID3, el valor es <span class="codeph"> AdobePSDK.TimedMetadataType.ID3 </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> hora </span> </p> </td> 
   <td colname="col2"> <p> Hora del reproductor en el que se detectaron estos metadatos cronometrados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> id </span> </p> </td> 
   <td colname="col2"> <p>ID del <span class="codeph"> TimedMetadata </span> objeto. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> name </span> </p> </td> 
   <td colname="col2"> <p>Nombre de <span class="codeph"> TimedMetadata </span> objeto. Para los metadatos de ID3, el valor es "ID3". </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> content </span> </p> </td> 
   <td colname="col2"> <p>El contenido de metadatos cronometrados. Para las etiquetas ID3, este valor representa la matriz de bytes serializados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> metadatos </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> TimedMetadata </span> información procesada, que es una instancia de <span class="codeph"> AdobePSDK.Metadata </span> donde se almacenan las tramas ID3. </p> <p> <p>Nota: Para Safari <span class="codeph"> video </span> , los datos de marco concretos de la etiqueta ID3 se exponen en forma de objeto a través de una etiqueta <span class="codeph"> AdobePSDK.Metadata </span> mientras que para otros exploradores, los datos de trama de la etiqueta ID3 se exponen en forma de matriz de bytes a través de <span class="codeph"> AdobePSDK.Metadata </span> objeto. </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

&#x200B;

Las distintas etiquetas ID3 almacenadas en `TimedMetadata` La aplicación puede recuperarla de las dos maneras siguientes:

* En AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, detector de eventos.

  ```
  var isSafari = function () { 
      var nAgt = navigator.userAgent; 
      var appName = navigator.appName; 
      if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
          (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
          (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
          (nAgt.indexOf('Chrome') === -1) && // is not chrome 
          (nAgt.indexOf('Safari') !== -1) //is Safari 
      ){ 
          return true; 
      } 
      return false; 
  }; 
  var hex2a = function (hex, offset, max) { 
      var str = ''; 
      if (!hex) 
          return str; 
      for (var i = offset; i < hex.length && i < offset + max; i++) 
          str += String.fromCharCode(hex[i]); 
      return str; 
  }; 
  var mediaPlayer = new AdobePSDK.MediaPlayer(); 
  mediaPlayer.addEventListener( AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE ,function(event){ 
      var td = event.timedMetadata; 
      if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
          var md = td.metadata; 
          var keySet = md.keySet; 
          var onSafari = isSafari(); 
          if(keySet && keySet.length){ 
              var msg = ''; 
              for(var j = 0; j < keySet.length; j++){ 
                  var idTag = keySet[j]; 
                  msg += idTag; 
                  if(idTag.indexOf("T") == 0){ 
                      /* text frame*/ 
                      if(onSafari){ 
                          /* text frame data is exposed in object format 
                           * where corresponding text data is exposed through 
                           * data key of text frame data object 
                           * */ 
                          var frameDataObject = md.getObject(idTag); 
                          msg += " : " + frameDataObject.data; 
                      } else { 
                          var buff = md.getByteArray(idTag); 
                          msg += " : " + hex2a(buff, 0, buff.length - 1); 
                      } 
                  } 
                  msg += " ; "; 
              } 
          } 
      } 
  }); 
  ```

* Uso del `MediaPlayerItem`de `timedMetadata` propiedad.

  ```
  var isSafari = function () { 
      var nAgt = navigator.userAgent; 
      var appName = navigator.appName; 
      if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
          (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
          (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
          (nAgt.indexOf('Chrome') === -1) && // is not chrome 
          (nAgt.indexOf('Safari') !== -1) //is Safari 
      ){ 
          return true; 
      } 
      return false; 
  }; 
  var hex2a = function (hex, offset, max) { 
      var str = ''; 
      if (!hex) 
          return str; 
      for (var i = offset; i < hex.length && i < offset + max; i++) 
          str += String.fromCharCode(hex[i]); 
      return str; 
  }; 
  var timedMetadataList = player.currentItem.timedMetadata; 
  for(var i = 0; i < timedMetadataList.length; i++){ 
      var td = timedMetadataList[i]; 
      if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
          var md = td.metadata; 
          var keySet = md.keySet; 
          var onSafari = isSafari(); 
          if(keySet && keySet.length){ 
              var msg = ''; 
              for(var j = 0; j < keySet.length; j++){ 
                  var idTag = keySet[j]; 
                  msg += idTag; 
                  if(idTag.indexOf("T") == 0){ 
                      /* text frame*/ 
                      if(onSafari){ 
                          /* text frame data is exposed in object format 
                           * where corresponding text data is exposed through 
                           * data key of text frame data object 
                           * */ 
                          var frameDataObject = md.getObject(idTag); 
                          msg += " : " + frameDataObject.data; 
                      } else { 
                          var buff = md.getByteArray(idTag); 
                          msg += " : " + hex2a(buff, 0, buff.length - 1); 
                      } 
                  } 
                  msg += " ; "; 
              } 
          } 
      } 
  } 
  ```
