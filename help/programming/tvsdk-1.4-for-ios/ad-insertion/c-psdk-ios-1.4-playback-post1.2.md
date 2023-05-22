---
description: El comportamiento de la reproducción de contenido se ve afectado por la búsqueda, la pausa y la inclusión de publicidad.
title: Comportamiento de reproducción predeterminado y personalizado con anuncios
exl-id: bd92b58a-fc71-41de-a80e-19002d66246f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Comportamiento de reproducción predeterminado y personalizado con anuncios{#default-and-customized-playback-behavior-with-ads}

El comportamiento de la reproducción de contenido se ve afectado por la búsqueda, la pausa y la inclusión de publicidad.

Para anular el comportamiento predeterminado, utilice `PTAdPolicySelector`.

>[!IMPORTANT]
>
>Para VOD y streaming en directo o lineal, no se pueden revisar los ajustes de línea de tiempo. Esto significa que un anuncio no se puede eliminar de la cronología una vez reproducido. Si el usuario hace una búsqueda, el mismo anuncio se reproduce de nuevo aunque la política normal hubiera sido eliminarlo.

>[!IMPORTANT]
>
>TVSDK no proporciona una forma de deshabilitar la búsqueda durante los anuncios. El Adobe recomienda configurar la aplicación para deshabilitar la búsqueda durante los anuncios.

En la tabla siguiente se describe cómo gestiona TVSDK los anuncios y las pausas publicitarias durante la reproducción:

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Actividad de vídeo </th> 
   <th colname="col2" class="entry"> Directiva de comportamiento predeterminada de TVSDK </th> 
   <th colname="col3" class="entry">Personalización disponible mediante <span class="codeph"> PTAdPolicySelector</span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Durante la reproducción normal, se produce una pausa publicitaria. </td> 
   <td colname="col2"></td> 
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
   <td colname="col3">Seleccione cuál de los saltos omitidos se reproducirá con <span class="codeph"> selectAdBreaksToPlay</span> y determine qué pausas ya se han visto utilizando <span class="codeph"> PTAdBreak.isWatched</span>. <p> <p>Importante: De forma predeterminada, TVSDK marca una pausa publicitaria como vigilada inmediatamente después de introducir el primer anuncio en la pausa publicitaria. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante o hacia atrás en una o más pausas publicitarias y pasa a una pausa publicitaria vigilada. </td> 
   <td colname="col2"> Omite la pausa publicitaria y busca la posición inmediatamente después de la pausa publicitaria. </td> 
   <td colname="col3">Especifique una política de publicidad diferente para la pausa publicitaria (con el estado de observación establecido en verdadero) y para el anuncio específico en el que la búsqueda ha finalizado utilizando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación hace una búsqueda hacia delante sobre los anuncios insertados mediante marcadores de publicidad personalizados. </td> 
   <td colname="col2"> Pasa a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>
