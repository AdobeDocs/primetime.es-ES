---
description: El comportamiento de la reproducción de contenido se ve afectado por la búsqueda, la pausa y la inclusión de publicidad.
title: Comportamiento de reproducción predeterminado y personalizado con anuncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Comportamiento de reproducción predeterminado y personalizado con anuncios{#default-and-customized-playback-behavior-with-ads}

El comportamiento de la reproducción de contenido se ve afectado por la búsqueda, la pausa y la inclusión de publicidad.

Para anular el comportamiento predeterminado, utilice `PTAdPolicySelector`.

>[!IMPORTANT]
>
>Para VOD y flujo en directo/lineal, los ajustes de línea de tiempo no se pueden revisar. Esto significa que un anuncio no se puede eliminar de la cronología después de reproducirse. Si el usuario vuelve a buscar, se reproduce el mismo anuncio aunque la política normal hubiera sido eliminarlo.

>[!IMPORTANT]
>
>TVSDK no proporciona una forma de deshabilitar la búsqueda durante los anuncios. Adobe recomienda configurar la aplicación para deshabilitar la búsqueda durante los anuncios.

En la tabla siguiente se describe cómo TVSDK gestiona los anuncios y las pausas publicitarias durante la reproducción:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Actividad de vídeo </th> 
   <th colname="col2" class="entry"> Política de comportamiento predeterminada de TVSDK </th> 
   <th colname="col3" class="entry">Personalización disponible mediante <span class="codeph"> PTAdPolicySelector</span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante la reproducción normal, se encuentra una pausa publicitaria. </td> 
   <td colname="col2"></td> 
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
   <td colname="col3">Seleccione cuál de los saltos omitidos para reproducir con <span class="codeph"> selectAdBreaksToPlay</span> y determine qué saltos ya se han visto utilizando <span class="codeph"> PTAdBreak.isWatched</span>. <p> <p>Importante:  De forma predeterminada, TVSDK marca una pausa publicitaria como se observa inmediatamente después de introducir el primer anuncio en la pausa publicitaria. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca avanzar o retroceder en una o más pausas publicitarias y cae en una pausa publicitaria observada. </td> 
   <td colname="col2"> Omite la pausa publicitaria y busca la posición inmediatamente después de la pausa publicitaria. </td> 
   <td colname="col3">Especifique una política de publicidad diferente para la pausa publicitaria (con el estado visto establecido en verdadero) y para el anuncio específico donde la búsqueda terminó usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante anuncios que se insertaron mediante marcadores de anuncios personalizados. </td> 
   <td colname="col2"> Pasa a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>

