---
description: El comportamiento de la reproducción de contenido se ve afectado por la llamada a otro punto del contenido, la pausa, el avance rápido o el rebobinado (modo de reproducción engañosa) y la inclusión de publicidad.
title: Comportamiento de reproducción predeterminado y personalizado con anuncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# Comportamiento de reproducción predeterminado y personalizado con anuncios{#default-and-customized-playback-behavior-with-ads}

El comportamiento de la reproducción de contenido se ve afectado por la llamada a otro punto del contenido, la pausa, el avance rápido o el rebobinado (modo de reproducción engañosa) y la inclusión de publicidad.

Para anular el comportamiento predeterminado, utilice `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>El SDK de explorador no proporciona una forma de deshabilitar la búsqueda durante los anuncios. Adobe recomienda configurar la aplicación para deshabilitar la búsqueda durante los anuncios.

En la tabla siguiente se describe cómo el TVSDK del explorador gestiona los anuncios y las pausas publicitarias durante la reproducción:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Actividad de vídeo </th> 
   <th colname="col2" class="entry"> Política de comportamiento predeterminada de TVSDK del explorador </th> 
   <th colname="col3" class="entry">Personalización disponible mediante <span class="codeph"> AdBreakPolicySelector </span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante la reproducción normal, se encuentra una pausa publicitaria. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> En directo/lineal, reproduce la pausa publicitaria, aunque la pausa publicitaria ya se haya visto. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">En el caso de VOD, reproduce la pausa publicitaria y marca la pausa publicitaria como se vio. </li> 
    </ul> </td> 
   <td colname="col3">Especifique una política diferente para la pausa publicitaria utilizando <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante durante las pausas publicitarias en el contenido principal. </td> 
   <td colname="col2"> Reproduce la última pausa publicitaria no visualizada que se omitió y reanuda la reproducción en la posición deseada cuando se completa la reproducción de la pausa. </td> 
   <td colname="col3">Seleccione qué salto omitido reproducir utilizando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia atrás más de las pausas publicitarias en el contenido principal. </td> 
   <td colname="col2"> Pasa a la posición de búsqueda deseada sin reproducir pausas publicitarias. </td> 
   <td colname="col3">Seleccione qué salto omitido reproducir utilizando <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante en una pausa publicitaria. </td> 
   <td colname="col2"> Se reproduce desde el principio del anuncio en el que finalizó la búsqueda. </td> 
   <td colname="col3">Especifique una política de publicidad diferente para la pausa publicitaria y para el anuncio específico donde la búsqueda terminó usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia atrás en una pausa publicitaria. </td> 
   <td colname="col2"> Se reproduce desde el principio del anuncio en el que finalizó la búsqueda. </td> 
   <td colname="col3">Especifique una política de publicidad diferente para la pausa publicitaria y para el anuncio específico en el que la búsqueda terminó usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante o hacia atrás las pausas publicitarias vistas en el contenido principal. </td> 
   <td colname="col2"> Si ya se ha visto la última pausa publicitaria omitida, se salta a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3">Seleccione cuál de los saltos omitidos para reproducir con <span class="codeph"> selectAdBreaksToPlay</span> y determine qué saltos ya se han visto con <span class="codeph"> isWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca avanzar o retroceder en una o más pausas publicitarias y cae en una pausa publicitaria observada. </td> 
   <td colname="col2"> Omite la pausa publicitaria y busca la posición inmediatamente después de la pausa publicitaria. </td> 
   <td colname="col3">Especifique una política de publicidad diferente para la pausa publicitaria (con el estado visto establecido en verdadero) y para el anuncio específico donde la búsqueda terminó usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante anuncios que se insertaron mediante marcadores de anuncios personalizados. </td> 
   <td colname="col2"> Pasa a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3">Para obtener más información, consulte <a href="../../browser-tvsdk-2.4/content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Administrar búsqueda al utilizar la barra de búsqueda</a> </td> 
  </tr> 
 </tbody> 
</table>

## Configuración de comportamientos de publicidad personalizados {#section_custom_ad_behaviors}

Puede establecer su comportamiento preferido en la fábrica de contenido publicitario del método `retrieveAdPolicySelectorCallbackFunc` . Puede utilizar los métodos `selectPolicyForAdBreak`, `selectWatchedPolicyForAdBreak`, `selectPolicyForSeekIntoAd` y `selectAdBreaksToPlay` en la fábrica de contenido para seleccionar una política.
