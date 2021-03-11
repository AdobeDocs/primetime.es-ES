---
description: Quality of service (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
title: Seguimiento en el nivel de fragmento mediante información de carga
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Rastrear a nivel de fragmento utilizando información de carga{#track-at-the-fragment-level-using-load-information}

Quality of service (QoS) ofrece una vista detallada del rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

TVSDK también proporciona información sobre los siguientes recursos descargados:

1. Archivos de lista de reproducción/manifiesto
1. Fragmentos de archivo
1. Información de seguimiento de archivos

   Puede leer información sobre la calidad del servicio (QoS) acerca de los recursos descargados, como fragmentos y pistas, desde la clase `LoadInfo`.

1. Implemente el detector de eventos de llamada de retorno `onLoadInfo`.
1. Registre el detector de eventos, al que llama TVSDK cada vez que se descarga un fragmento.
1. Lea los datos de interés del parámetro `LoadInfo` que se pasa a la rellamada.

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
      <td colname="col01"> <span class="codeph"> downloadDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> <p>Duración de la descarga en milisegundos. </p> <p>TVSDK no diferencia entre el tiempo que tardó el cliente en conectarse al servidor y el tiempo que tardó en descargar el fragmento completo. Por ejemplo, si la descarga de un segmento de 10 MB tarda 8 segundos, TVSDK proporciona esa información, pero no le indica que se tardaron 4 segundos hasta el primer byte y otros 4 segundos en descargar el fragmento completo. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> Duración del contenido de los fragmentos descargados en milisegundos. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> Índice de periodo de tiempo asociado con el recurso descargado. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> size  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> El tamaño del recurso descargado en bytes. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> Índice de la pista correspondiente, si se conoce; de lo contrario, 0. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena  </span> </td> 
      <td colname="col2"> el nombre de la pista correspondiente, si se conoce; de lo contrario, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena  </span> </td> 
      <td colname="col2"> el tipo de pista correspondiente, si se conoce; de lo contrario, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type  </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena  </span> </td> 
      <td colname="col2"> Qué ha descargado TVSDK. Uno de los siguientes: 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFIESTO: lista de reproducción/manifiesto </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">FRAGMENTO: Un fragmento </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK: fragmento asociado a una pista específica </li> 
      </ul> A veces, es posible que no sea posible detectar el tipo de recurso. Si esto ocurre, se devuelve FILE. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena  </span> </td> 
      <td colname="col2"> Dirección URL que señala al recurso descargado. </td> 
      </tr> 
    </tbody> 
   </table>
