---
description: El comportamiento de la reproducción de contenido se ve afectado por la búsqueda, la pausa, el avance o el rebobinado rápidos y la publicidad.
title: Comportamiento de reproducción predeterminado y personalizado con anuncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# Comportamiento de reproducción predeterminado y personalizado con anuncios {#default-and-customized-playback-behavior-with-ads}

El comportamiento de la reproducción de contenido se ve afectado por la búsqueda, la pausa, el avance o el rebobinado rápidos y la publicidad.

Para anular el comportamiento predeterminado, utilice `AdBreakPolicySelector` .

>[!IMPORTANT]
>
>TVSDK no proporciona una forma de deshabilitar la búsqueda durante los anuncios. Adobe recomienda configurar la aplicación para deshabilitar la búsqueda durante los anuncios.

Este es el comportamiento de reproducción del contenido en directo/lineal:

* La reanudación de la reproducción después de una pausa provoca la reproducción del contenido que se almacenó en búfer en el momento de la pausa.

   Si la posición de reanudación sigue en el intervalo de reproducción, la reproducción debe ser continua. De lo contrario, TVSDK salta al nuevo punto activo. También puede realizar una operación de búsqueda y seleccionar un punto de reproducción diferente.
* TVSDK resuelve los anuncios entre señales después de la posición en la que la aplicación entra en reproducción activa.

   La reproducción comienza después de que se resuelva la primera señal. El valor predeterminado para introducir la reproducción en directo es el punto activo del cliente, pero puede elegir una posición diferente. Todas las señales antes de la posición inicial se resuelven después de que la aplicación realice una búsqueda en la ventana DVR.

En la tabla siguiente se describe cómo TVSDK gestiona los anuncios y las pausas publicitarias durante la reproducción:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Actividad de vídeo</b> </th> 
   <th colname="col2" class="entry"> <b>Política de comportamiento predeterminada de TVSDK</b> </th> 
   <th colname="col3" class="entry"><b>Personalización disponible mediante  <span class="codeph"> AdBreakPolicySelector</b></span> </th> 
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
   <td colname="col3">Seleccione cuál de los saltos omitidos para reproducir con <span class="codeph"> selectAdBreaksToPlay</span> y determine qué pausas ya se han visto con <span class="codeph"> AdBreak.isWatched</span> . <p>Importante:  De forma predeterminada, TVSDK marca una pausa publicitaria como se observa inmediatamente después de introducir el primer anuncio en la pausa publicitaria. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca avanzar o retroceder en una o más pausas publicitarias y cae en una pausa publicitaria observada. </td> 
   <td colname="col2"> Omite la pausa publicitaria y busca la posición inmediatamente después de la pausa publicitaria. </td> 
   <td colname="col3">Especifique una política de publicidad diferente para la pausa publicitaria (con el estado visto establecido en verdadero) y para el anuncio específico donde la búsqueda terminó usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Su aplicación entra en juego con trucos (modo DVR). La velocidad de reproducción puede ser negativa (rebobinado) o buena que 1 (avance rápido). </td> 
   <td colname="col2"> Omite todos los anuncios durante el avance rápido o el rebobinado, reproduce la última pausa omitida después de que finalice la reproducción del truco y omite la posición de reproducción del truco seleccionada por el usuario cuando esa pausa termina de reproducirse. </td> 
   <td colname="col3">Seleccione cuál de los saltos omitidos para reproducir después de que termine la reproducción de trucos con <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante anuncios que se insertaron mediante marcadores de anuncios personalizados. </td> 
   <td colname="col2"> Pasa a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3">Para obtener más información, consulte <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md" format="dita" scope="local"> Mostrar una barra de depuración con la posición de reproducción actual</a>. </td> 
  </tr> 
 </tbody> 
</table>

