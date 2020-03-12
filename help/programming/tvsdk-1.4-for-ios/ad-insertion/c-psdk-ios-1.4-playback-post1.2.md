---
description: El comportamiento de la reproducción de medios se ve afectado por la búsqueda, la pausa y la inclusión de publicidad.
seo-description: El comportamiento de la reproducción de medios se ve afectado por la búsqueda, la pausa y la inclusión de publicidad.
seo-title: Comportamiento de reproducción predeterminado y personalizado con anuncios
title: Comportamiento de reproducción predeterminado y personalizado con anuncios
uuid: cc996e5c-bee2-451b-96cb-088df1694188
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Comportamiento de reproducción predeterminado y personalizado con anuncios{#default-and-customized-playback-behavior-with-ads}

El comportamiento de la reproducción de medios se ve afectado por la búsqueda, la pausa y la inclusión de publicidad.

Para anular el comportamiento predeterminado, utilice `PTAdPolicySelector`.

>[!IMPORTANT]
>
>En el caso de VOD y transmisión en directo/lineal, los ajustes de línea de tiempo no se pueden revisar. Esto significa que un anuncio no se puede eliminar de la línea de tiempo después de reproducirse. Si el usuario busca de nuevo, el mismo anuncio se reproduce incluso si la política normal hubiera sido eliminarlo.

>[!IMPORTANT]
>
>TVSDK no proporciona una manera de desactivar la búsqueda durante las publicidades. Adobe recomienda configurar la aplicación para que deshabilite la búsqueda durante las publicidades.

En la tabla siguiente se describe cómo TVSDK gestiona anuncios y saltos de publicidad durante la reproducción:

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
   <td colname="col3">Especifique una directiva diferente para el desglose de publicidad mediante <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia adelante más allá de las interrupciones publicitarias en el contenido principal. </td> 
   <td colname="col2"> Reproduce la última pausa publicitaria no observada que se omitió y reanuda la reproducción en la posición de búsqueda deseada cuando se termina la reproducción de los saltos. </td> 
   <td colname="col3">Seleccione qué salto omitido se reproducirá mediante <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia atrás en los saltos de publicidad en el contenido principal. </td> 
   <td colname="col2"> Salta a la posición de búsqueda deseada sin reproducir saltos de publicidad. </td> 
   <td colname="col3">Seleccione qué salto omitido se reproducirá mediante <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
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
   <td colname="col3">Seleccione cuál de los saltos omitidos se reproducirá con <span class="codeph"> selectAdBreaksToPlay</span> y determine qué saltos ya se han visto mediante <span class="codeph"> PTAdBreak.isWatched</span>. <p> <p>Importante:  De forma predeterminada, TVSDK marca una pausa publicitaria como se observa inmediatamente después de introducir el primer anuncio en la pausa publicitaria. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca avanzar o retroceder en uno o más saltos de publicidad y cae en una pausa publicitaria observada. </td> 
   <td colname="col2"> Omite la pausa publicitaria y busca la posición inmediatamente después de la pausa publicitaria. </td> 
   <td colname="col3">Especifique una directiva de publicidad diferente para la pausa publicitaria (con el estado visto establecido en true) y para la publicidad específica en la que la búsqueda terminó usando <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> La aplicación busca hacia delante publicidades insertadas mediante marcadores de publicidad personalizados. </td> 
   <td colname="col2"> Pasa a la posición de búsqueda seleccionada por el usuario. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>

