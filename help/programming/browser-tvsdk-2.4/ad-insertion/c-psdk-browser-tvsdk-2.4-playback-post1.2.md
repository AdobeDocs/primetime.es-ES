---
description: El comportamiento de la reproducción de medios se ve afectado por la búsqueda, pausa, avance rápido o rebobinado (modo de juego truco) y la inclusión de la publicidad.
seo-description: El comportamiento de la reproducción de medios se ve afectado por la búsqueda, pausa, avance rápido o rebobinado (modo de juego truco) y la inclusión de la publicidad.
seo-title: Comportamiento de reproducción predeterminado y personalizado con anuncios
title: Comportamiento de reproducción predeterminado y personalizado con anuncios
uuid: 58f11167-a764-4647-8490-05ca66eb6c47
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# Comportamiento de reproducción predeterminado y personalizado con anuncios{#default-and-customized-playback-behavior-with-ads}

El comportamiento de la reproducción de medios se ve afectado por la búsqueda, pausa, avance rápido o rebobinado (modo de juego truco) y la inclusión de la publicidad.

Para anular el comportamiento predeterminado, utilice `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>El SDK de explorador no proporciona una manera de deshabilitar la búsqueda durante las publicidades. Adobe recomienda configurar la aplicación para que deshabilite la búsqueda durante las publicidades.

En la tabla siguiente se describe cómo el SDK de TVSDK del explorador gestiona anuncios y saltos de publicidad durante la reproducción:

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
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> En directo/lineal, reproduce la pausa publicitaria, incluso si la pausa publicitaria ya se ha visto. </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">En el caso de VOD, reproduce la pausa publicitaria y marca la pausa publicitaria como se vio. </li> 
    </ul> </td> 
   <td colname="col3">Especifique una directiva diferente para la pausa publicitaria mediante <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia adelante más allá de las interrupciones publicitarias en el contenido principal. </td> 
   <td colname="col2"> Reproduce la última pausa publicitaria no observada que se omitió y reanuda la reproducción en la posición de búsqueda deseada cuando se termina la reproducción de los saltos. </td> 
   <td colname="col3">Seleccione qué salto omitido se debe reproducir mediante <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia atrás en los saltos de publicidad en el contenido principal. </td> 
   <td colname="col2"> Salta a la posición de búsqueda deseada sin reproducir saltos de publicidad. </td> 
   <td colname="col3">Seleccione qué salto omitido se debe reproducir mediante <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante en una pausa publicitaria. </td> 
   <td colname="col2"> Se reproduce desde el principio del anuncio en el que finalizó la búsqueda. </td> 
   <td colname="col3">Especifique una directiva de publicidad diferente para la pausa publicitaria y para la publicidad específica en la que la búsqueda terminó usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia atrás en una pausa publicitaria. </td> 
   <td colname="col2"> Se reproduce desde el principio del anuncio en el que finalizó la búsqueda. </td> 
   <td colname="col3">Especifique una directiva de publicidad diferente para la pausa publicitaria y para la publicidad específica en la que la búsqueda terminó usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca avanzar o retroceder en los saltos de publicidad vistos en el contenido principal. </td> 
   <td colname="col2"> Si la última pausa publicitaria omitida ya se ha visto, se salta a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3">Seleccione cuál de los saltos omitidos se reproducirá con <span class="codeph"> selectAdBreaksToPlay</span> y determine qué saltos ya se han visto con <span class="codeph"> isWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca avanzar o retroceder en uno o más saltos de publicidad y cae en una pausa publicitaria observada. </td> 
   <td colname="col2"> Omite la pausa publicitaria y busca la posición inmediatamente después de la pausa publicitaria. </td> 
   <td colname="col3">Especifique una directiva de publicidad diferente para la pausa publicitaria (con el estado visto establecido en true) y para la publicidad específica en la que la búsqueda terminó usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante publicidades insertadas mediante marcadores de publicidad personalizados. </td> 
   <td colname="col2"> Pasa a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3">Para obtener más información, consulte <a href="../../browser-tvsdk-2.4/content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Administrar búsqueda al utilizar la barra de búsqueda</a> </td> 
  </tr> 
 </tbody> 
</table>

## Configuración de comportamientos de publicidad personalizados {#section_custom_ad_behaviors}

Puede establecer el comportamiento preferido en la fábrica de contenido de publicidad en el método `retrieveAdPolicySelectorCallbackFunc`. Puede utilizar los métodos `selectPolicyForAdBreak`, `selectWatchedPolicyForAdBreak`, `selectPolicyForSeekIntoAd` y `selectAdBreaksToPlay` en la fábrica de contenido para seleccionar una política.
