---
description: El comportamiento de la reproducción de medios se ve afectado por la búsqueda, pausa, avance rápido o rebobinado (modo de juego truco) y la inclusión de la publicidad.
seo-description: El comportamiento de la reproducción de medios se ve afectado por la búsqueda, pausa, avance rápido o rebobinado (modo de juego truco) y la inclusión de la publicidad.
seo-title: Comportamiento de reproducción predeterminado y personalizado con anuncios
title: Comportamiento de reproducción predeterminado y personalizado con anuncios
uuid: b977d7b5-bbae-4af4-92a7-0fdbffb08785
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# Comportamiento de reproducción predeterminado y personalizado con anuncios {#default-and-customized-playback-behavior-with-ads}

El comportamiento de la reproducción de medios se ve afectado por la búsqueda, pausa, avance rápido o rebobinado (modo de juego truco) y la inclusión de la publicidad.

Para anular el comportamiento predeterminado, utilice `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>TVSDK no proporciona una manera de desactivar la búsqueda durante las publicidades. Adobe recomienda configurar la aplicación para que deshabilite la búsqueda durante las publicidades.

Este es el comportamiento de reproducción del contenido en directo o lineal:

* Si se reanuda la reproducción después de una pausa, se producirá la reproducción del contenido que se almacenó en el búfer en el momento de la pausa.

   Si la posición de reanudación sigue en el rango de reproducción, la reproducción debe ser continua. De lo contrario, TVSDK salta al nuevo punto de lanzamiento. También puede realizar una operación de búsqueda y seleccionar otro punto de reproducción.
* TVSDK resuelve las publicidades entre señales después de la posición en la que la aplicación entra en la reproducción en directo.

   La reproducción comienza después de que se resuelva la primera señal. El valor predeterminado para la reproducción en directo es el punto activo del cliente, pero puede elegir una posición diferente. Todas las señales anteriores a la posición inicial se resuelven después de que la aplicación realiza una búsqueda en la ventana DVR.

En la tabla siguiente se describe cómo TVSDK gestiona anuncios y saltos de publicidad durante la reproducción:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Actividad de vídeo </th> 
   <th colname="col2" class="entry"> Directiva de comportamiento predeterminada de TVSDK </th> 
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
   <td colname="col3">Seleccione cuál de los saltos omitidos se reproducirá mediante <span class="codeph"> selectAdBreaksToPlay</span> y determine qué saltos ya se han visto mediante <span class="codeph"> AdBreak.isWatched</span>. <p>Importante:  De forma predeterminada, TVSDK marca una pausa publicitaria como se observa inmediatamente después de introducir el primer anuncio en la pausa publicitaria. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca avanzar o retroceder en uno o más saltos de publicidad y cae en una pausa publicitaria observada. </td> 
   <td colname="col2"> Omite la pausa publicitaria y busca la posición inmediatamente después de la pausa publicitaria. </td> 
   <td colname="col3">Especifique una directiva de publicidad diferente para la pausa publicitaria (con el estado visto establecido en true) y para la publicidad específica en la que la búsqueda terminó usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Su aplicación entra en juego con trucos (modo DVR). La velocidad de reproducción puede ser negativa (rebobinado) o buena de 1 (avance rápido). </td> 
   <td colname="col2"> Omite todos los anuncios durante el avance rápido o el rebobinado, reproduce el último salto omitido después de que finalice la reproducción con trucos y omite la posición de reproducción con trucos seleccionada por el usuario cuando dicho salto termina la reproducción. </td> 
   <td colname="col3">Seleccione cuál de los saltos omitidos se reproducirá después de que termine la reproducción mediante <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante publicidades insertadas mediante marcadores de publicidad personalizados. </td> 
   <td colname="col2"> Pasa a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3">Para obtener más información, consulte <a href="../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-seek-scrub-bar-display.md">Visualización de una barra de búsqueda con borrado con la posición de reproducción actual</a>. </td> 
  </tr> 
 </tbody> 
</table>

