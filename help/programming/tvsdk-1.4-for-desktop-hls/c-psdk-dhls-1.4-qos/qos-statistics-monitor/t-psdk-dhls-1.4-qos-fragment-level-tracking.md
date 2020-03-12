---
description: Puede leer información de calidad de servicio (QoS) sobre los recursos descargados, como fragmentos y pistas, desde la clase LoadInformation.
seo-description: Puede leer información de calidad de servicio (QoS) sobre los recursos descargados, como fragmentos y pistas, desde la clase LoadInformation.
seo-title: Rastrear en el nivel de fragmento mediante la información de carga
title: Rastrear en el nivel de fragmento mediante la información de carga
uuid: 41fb2b90-3531-4cc5-bf9b-01ccae04d2fd
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Rastrear en el nivel de fragmento mediante la información de carga{#track-at-the-fragment-level-using-load-information}

Puede leer información de calidad de servicio (QoS) sobre los recursos descargados, como fragmentos y pistas, desde la clase LoadInformation.

1. Implemente el detector de eventos de `onLoadInformationAvailable` llamada de retorno.

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. Registre el detector de eventos, al que llama TVSDK cada vez que se descarga un fragmento.

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. Lea los datos de interés del `LoadInformation` que se pasa a la llamada de retorno.

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> Propiedad </th> 
      <th colname="col1" class="entry"> Tipo </th> 
      <th colname="col2" class="entry"> Descripción </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> <p>Duración de la descarga en milisegundos. </p> <p>TVSDK no diferencia entre el tiempo que tardó el cliente en conectarse al servidor y el tiempo que tardó en descargar el fragmento completo. Por ejemplo, si un segmento de 10 MB tarda 8 segundos en descargarse, TVSDK proporciona esa información, pero no le indica que pasaron 4 segundos hasta el primer byte y otros 4 segundos hasta descargar el fragmento completo. </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> Duración media de los fragmentos descargados en milisegundos. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> size </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> El tamaño del recurso descargado en bytes. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> Índice de la pista correspondiente, si se conoce; en caso contrario, 0. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>Cadena </p> </td> 
      <td colname="col2"> El nombre de la pista correspondiente, si se conoce; en caso contrario, null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>Cadena </p> </td> 
      <td colname="col2"> El tipo de pista correspondiente, si se conoce; en caso contrario, null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <p>Cadena </p> </td> 
      <td colname="col2"> Qué TVSDK se ha descargado. Uno de los siguientes: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFIESTO: una lista de reproducción/manifiesto </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAGMENTO: Un fragmento </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK: fragmento asociado a una pista específica </li> 
      </ul> A veces puede que no sea posible detectar el tipo de recurso. Si esto sucede, se devuelve FILE. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>Cadena </p> </td> 
      <td colname="col2"> Dirección URL que apunta al recurso descargado. </td> 
   </tr> 
   </tbody> 
   </table>
