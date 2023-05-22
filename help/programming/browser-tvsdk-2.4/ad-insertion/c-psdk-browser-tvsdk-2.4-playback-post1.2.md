---
description: El comportamiento de la reproducción de contenido se ve afectado por la búsqueda, la pausa, el avance rápido o el rebobinado (modo de reproducción con trucos) y la inclusión de publicidad.
title: Comportamiento de reproducción predeterminado y personalizado con anuncios
exl-id: 56544683-28a3-4720-bfd8-946cb09880aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Comportamiento de reproducción predeterminado y personalizado con anuncios{#default-and-customized-playback-behavior-with-ads}

El comportamiento de la reproducción de contenido se ve afectado por la búsqueda, la pausa, el avance rápido o el rebobinado (modo de reproducción con trucos) y la inclusión de publicidad.

Para anular el comportamiento predeterminado, utilice `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>El TVSDK del explorador no proporciona una forma de deshabilitar la búsqueda durante los anuncios. El Adobe recomienda configurar la aplicación para deshabilitar la búsqueda durante los anuncios.

En la tabla siguiente se describe cómo gestiona TVSDK del explorador los anuncios y las pausas publicitarias durante la reproducción:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Actividad de vídeo </th> 
   <th colname="col2" class="entry"> Directiva de comportamiento predeterminada de TVSDK del explorador </th> 
   <th colname="col3" class="entry">Personalización disponible mediante <span class="codeph"> AdBreakPolicySelector </span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante la reproducción normal, se produce una pausa publicitaria. </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> Para anuncios en directo/lineales, reproduce la pausa publicitaria, incluso si ya se ha visto. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">En VOD, reproduce la pausa publicitaria y la marca como inspeccionada. </li> 
    </ul> </td> 
   <td colname="col3">Especificar una política diferente para la pausa publicitaria utilizando <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia adelante las pausas publicitarias en el contenido principal. </td> 
   <td colname="col2"> Reproduce la última pausa para anuncios no vistos que se omitió y reanuda la reproducción en la posición de búsqueda deseada cuando se completa la reproducción de la pausa(s). </td> 
   <td colname="col3">Seleccione el salto omitido que se reproducirá utilizando <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia atrás en las pausas publicitarias en el contenido principal. </td> 
   <td colname="col2"> Salta a la posición de búsqueda deseada sin pausas publicitarias. </td> 
   <td colname="col3">Seleccione el salto omitido que se reproducirá utilizando <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación intenta avanzar hasta una pausa publicitaria. </td> 
   <td colname="col2"> Reproduce desde el principio del anuncio en el que finalizó la búsqueda. </td> 
   <td colname="col3">Especifique una política de publicidad diferente para la pausa publicitaria y para el anuncio específico en el que la búsqueda ha finalizado utilizando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación retrocede hasta una pausa publicitaria. </td> 
   <td colname="col2"> Reproduce desde el principio del anuncio en el que finalizó la búsqueda. </td> 
   <td colname="col3">Especifique una política de anuncios diferente para la pausa publicitaria y para el anuncio específico en el que la búsqueda ha finalizado utilizando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante o hacia atrás en las pausas publicitarias vigiladas en el contenido principal. </td> 
   <td colname="col2"> Si la última pausa publicitaria omitida ya se ha visto, salta a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3">Seleccione cuál de los saltos omitidos se reproducirá con <span class="codeph"> selectAdBreaksToPlay</span> y determine qué pausas ya se han visto utilizando <span class="codeph"> isWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante o hacia atrás en una o más pausas publicitarias y pasa a una pausa publicitaria vigilada. </td> 
   <td colname="col2"> Omite la pausa publicitaria y busca la posición inmediatamente después de la pausa publicitaria. </td> 
   <td colname="col3">Especifique una política de publicidad diferente para la pausa publicitaria (con el estado de observación establecido en verdadero) y para el anuncio específico en el que la búsqueda ha finalizado utilizando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación hace una búsqueda hacia delante sobre los anuncios insertados mediante marcadores de publicidad personalizados. </td> 
   <td colname="col2"> Pasa a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3">Para obtener más información, consulte <a href="../../browser-tvsdk-2.4/content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Controlar la búsqueda al utilizar la barra de búsqueda</a> </td> 
  </tr> 
 </tbody> 
</table>

## Configuración de comportamientos de publicidad personalizados {#section_custom_ad_behaviors}

Puede establecer su comportamiento preferido en la fábrica de contenido de publicidad en `retrieveAdPolicySelectorCallbackFunc` método. Puede usar el complemento `selectPolicyForAdBreak`, `selectWatchedPolicyForAdBreak`, `selectPolicyForSeekIntoAd`, y `selectAdBreaksToPlay` métodos en el generador de contenido para seleccionar una directiva.
