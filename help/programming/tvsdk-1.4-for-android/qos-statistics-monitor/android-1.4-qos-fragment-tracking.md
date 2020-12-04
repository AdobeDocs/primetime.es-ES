---
description: Calidad de servicio (QoS) oferta una vista detallada sobre el rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
seo-description: Calidad de servicio (QoS) oferta una vista detallada sobre el rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.
seo-title: Rastrear en el nivel de fragmento mediante la información de carga
title: Rastrear en el nivel de fragmento mediante la información de carga
uuid: a6572823-d525-4ce0-806a-3feb20678cb0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---


# Rastree en el nivel de fragmento mediante información de carga{#track-at-the-fragment-level-using-load-information}

Calidad de servicio (QoS) oferta una vista detallada sobre el rendimiento del motor de vídeo. TVSDK proporciona estadísticas detalladas sobre la reproducción, el almacenamiento en búfer y los dispositivos.

TVSDK también proporciona información sobre los siguientes recursos descargados:

1. Archivos de lista de reproducción/manifiesto
1. Fragmentos de archivo
1. Información de seguimiento de archivos

   Puede leer información de calidad de servicio (QoS) sobre los recursos descargados, como fragmentos y pistas, desde la clase `LoadInfo`.

1. Implemente el detector de evento de rellamada `onLoadInfo`.
1. Registre el detector de evento, al que llama TVSDK cada vez que se descarga un fragmento.
1. Lea los datos de interés del parámetro `LoadInfo` que se pasa a la llamada de retorno.

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
      <td colname="col2"> <p>Duración de la descarga en milisegundos. </p> <p>TVSDK no diferencia entre el tiempo que tardó el cliente en conectarse al servidor y el tiempo que tardó en descargar el fragmento completo. Por ejemplo, si un segmento de 10 MB tarda 8 segundos en descargarse, TVSDK proporciona esa información, pero no le indica que pasaron 4 segundos hasta el primer byte y otros 4 segundos hasta descargar el fragmento completo. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> Duración media de los fragmentos descargados en milisegundos. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> Índice del período de tiempo asociado al recurso descargado. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> size  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> El tamaño del recurso descargado en bytes. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> Índice de la pista correspondiente, si se conoce; en caso contrario, 0. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena  </span> </td> 
      <td colname="col2"> El nombre de la pista correspondiente, si se conoce; en caso contrario, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena  </span> </td> 
      <td colname="col2"> El tipo de pista correspondiente, si se conoce; en caso contrario, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type  </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena  </span> </td> 
      <td colname="col2"> Qué TVSDK se ha descargado. Uno de los siguientes: 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFIESTO: una lista de reproducción/manifiesto </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">FRAGMENTO: Un fragmento </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK: fragmento asociado a una pista específica </li> 
      </ul> A veces puede que no sea posible detectar el tipo de recurso. Si esto sucede, se devuelve FILE. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <span class="codeph"> Cadena  </span> </td> 
      <td colname="col2"> Dirección URL que apunta al recurso descargado. </td> 
      </tr> 
    </tbody> 
   </table>
