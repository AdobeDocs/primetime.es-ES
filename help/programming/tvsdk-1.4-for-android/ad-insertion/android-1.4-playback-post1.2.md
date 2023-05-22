---
description: El comportamiento de la reproducción de contenido se ve afectado por la búsqueda, la pausa, el avance rápido o el rebobinado (modo de reproducción con trucos) y la inclusión de publicidad.
title: Comportamiento de reproducción predeterminado y personalizado con anuncios
exl-id: 242a94e7-acc1-4676-b8a7-9652d4fd1e7e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# Comportamiento de reproducción predeterminado y personalizado con anuncios {#default-and-customized-playback-behavior-with-ads}

El comportamiento de la reproducción de contenido se ve afectado por la búsqueda, la pausa, el avance rápido o el rebobinado (modo de reproducción con trucos) y la inclusión de publicidad.

Para anular el comportamiento predeterminado, utilice `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>TVSDK no proporciona una forma de deshabilitar la búsqueda durante los anuncios. El Adobe recomienda configurar la aplicación para deshabilitar la búsqueda durante los anuncios.

Este es el comportamiento de reproducción para contenido lineal/en directo:

* La reanudación de la reproducción después de una pausa provoca la reproducción del contenido que se almacenó en el búfer en el momento de la pausa.

   Si la posición de reanudación está todavía en el rango de reproducción, la reproducción debe ser continua. De lo contrario, TVSDK salta al nuevo punto de activación. También puede realizar una operación de búsqueda y seleccionar un punto de reproducción diferente.
* TVSDK resuelve los anuncios entre señales después de la posición en la que la aplicación entra en la reproducción en directo.

   La reproducción comienza después de que se haya resuelto la primera señal. El valor predeterminado para introducir la reproducción en directo es el punto en directo del cliente, pero puede elegir una posición diferente. Todas las señales antes de la posición inicial se resuelven después de que la aplicación realice una búsqueda en la ventana de DVR.

En la tabla siguiente se describe cómo gestiona TVSDK los anuncios y las pausas publicitarias durante la reproducción:

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
   <td colname="col3">Seleccione cuál de los saltos omitidos se reproducirá con <span class="codeph"> selectAdBreaksToPlay</span> y determine qué pausas ya se han visto utilizando <span class="codeph"> AdBreak.isWatched</span>. <p>Importante: De forma predeterminada, TVSDK marca una pausa publicitaria como vigilada inmediatamente después de introducir el primer anuncio en la pausa publicitaria. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante o hacia atrás en una o más pausas publicitarias y pasa a una pausa publicitaria vigilada. </td> 
   <td colname="col2"> Omite la pausa publicitaria y busca la posición inmediatamente después de la pausa publicitaria. </td> 
   <td colname="col3">Especifique una política de publicidad diferente para la pausa publicitaria (con el estado de observación establecido en verdadero) y para el anuncio específico en el que la búsqueda ha finalizado utilizando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación entra en el modo "trick-play" (modo DVR). La tasa de reproducción puede ser negativa (rebobinado) o buena que 1 (avance rápido). </td> 
   <td colname="col2"> Omite todos los anuncios durante el avance rápido o el rebobinado, reproduce la última pausa omitida después de que finalice la reproducción de trucos y salta a la posición de reproducción de trucos seleccionada por el usuario cuando esa pausa termina la reproducción. </td> 
   <td colname="col3">Seleccione cuál de los descansos omitidos se reproducirá una vez finalizada la reproducción con trucos <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación hace una búsqueda hacia delante sobre los anuncios insertados mediante marcadores de publicidad personalizados. </td> 
   <td colname="col2"> Pasa a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3">Para obtener más información, consulte <a href="../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-seek-scrub-bar-display.md">Mostrar una barra de desplazamiento de búsqueda con la posición de reproducción actual</a>. </td> 
  </tr> 
 </tbody> 
</table>
