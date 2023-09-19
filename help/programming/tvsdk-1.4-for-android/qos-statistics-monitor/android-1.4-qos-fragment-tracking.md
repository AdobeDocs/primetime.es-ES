---
description: Calidad de servicio (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
title: Seguimiento en el nivel de fragmento mediante información de carga
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Seguimiento en el nivel de fragmento mediante información de carga{#track-at-the-fragment-level-using-load-information}

Calidad de servicio (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

TVSDK también proporciona información sobre los siguientes recursos descargados:

1. Archivos de lista de reproducción/manifiesto
1. Fragmentos de archivo
1. Información de seguimiento para archivos

   Puede leer la información de calidad de servicio (QoS) sobre los recursos descargados, como fragmentos y pistas, desde el `LoadInfo` clase.

1. Implementación de `onLoadInfo` detector de eventos callback.
1. Registre el detector de eventos, al que TVSDK llama cada vez que se descarga un fragmento.
1. Lea los datos de interés de la `LoadInfo` parámetro que se pasa a la llamada de retorno.

   <table id="table_06BD536A23AB4A73B510998426BAE143"> 
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
      <td colname="col1"> <span class="codeph"> largo </span> </td> 
      <td colname="col2"> <p>Duración de la descarga en milisegundos. </p> <p>TVSDK no diferencia entre el tiempo que tardó el cliente en conectarse al servidor y el tiempo que tardó en descargar el fragmento completo. Por ejemplo, si un segmento de 10 MB tarda 8 segundos en descargarse, TVSDK proporciona esa información, pero no indica que hayan transcurrido 4 segundos hasta el primer byte y otros 4 segundos hasta descargar todo el fragmento. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <span class="codeph"> largo </span> </td> 
      <td colname="col2"> La duración de los medios de los fragmentos descargados en milisegundos. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> El índice del período de la cronología asociado al recurso descargado. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> talla </span> </td> 
      <td colname="col1"> <span class="codeph"> largo </span> </td> 
      <td colname="col2"> El tamaño del recurso descargado en bytes. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> El índice de la pista correspondiente, si se conoce; de lo contrario, 0. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena </span> </td> 
      <td colname="col2"> El nombre de la pista correspondiente, si se conoce; de lo contrario, es nulo. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena </span> </td> 
      <td colname="col2"> El tipo de la pista correspondiente, si se conoce; de lo contrario, es nulo. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena </span> </td> 
      <td colname="col2"> Lo que descargó TVSDK. Uno de los siguientes: 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFIESTO: una lista de reproducción/manifiesto </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">FRAGMENTO: un fragmento </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK: fragmento asociado a un seguimiento específico </li> 
      </ul> A veces, es posible que no se pueda detectar el tipo de recurso. Si esto sucede, se devuelve FILE. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena </span> </td> 
      <td colname="col2"> Dirección URL que señala al recurso descargado. </td> 
      </tr> 
    </tbody> 
   </table>
