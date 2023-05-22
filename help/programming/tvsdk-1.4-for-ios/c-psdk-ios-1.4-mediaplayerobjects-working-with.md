---
description: El objeto PTMediaPlayer representa el reproductor multimedia. PTMediaPlayerItem representa el audio o el vídeo del reproductor.
title: Trabajar con objetos MediaPlayer
exl-id: 0dd76446-0ea7-446d-a4bd-746128647173
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Trabajar con objetos MediaPlayer{#work-with-mediaplayer-objects}

El objeto PTMediaPlayer representa el reproductor multimedia. PTMediaPlayerItem representa el audio o el vídeo del reproductor.

## Acerca de la clase MediaPlayerItem {#section_B6F36C0462644F5C932C8AA2F6827071}

Una vez que un recurso multimedia se ha cargado correctamente, TVSDK crea una instancia de la variable `PTMediaPlayerItem` para proporcionar acceso a ese recurso.

El `PTMediaPlayer` resuelve el recurso multimedia, carga el archivo de manifiesto asociado y analiza el manifiesto. Esta es la parte asíncrona del proceso de carga de recursos. El `PTMediaPlayerItem` La instancia se genera después de que se haya resuelto el recurso y esta instancia es una versión resuelta de un recurso de medios. TVSDK proporciona acceso a los recién creados `PTMediaPlayerItem` instancia a través de `PTMediaPlayer.currentItem`.

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor de medios.

## Ciclo de vida del objeto MediaPlayer {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

Desde el momento en que crea el `PTMediaPlayer` hasta el momento en que la finaliza (reutiliza o elimina), esta instancia completa una serie de transiciones de un estado a otro.

Algunas operaciones solo se permiten cuando el reproductor está en un estado concreto. Por ejemplo, llamar a `play` in `PTMediaPlayerStatusCreated` no está permitido. Solo puede invocar este estado una vez que el reproductor haya alcanzado el `PTMediaPlayerStatusReady` estado.

Para trabajar con estados:

* Puede recuperar el estado actual del objeto MediaPlayer con `PTMediaPlayer.status`.
* La lista de estados se define en `PTMediaPlayerStatus`.

Diagrama de transición de estados para el ciclo de vida de una instancia de MediaPlayer:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

La siguiente tabla proporciona detalles adicionales:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> PTMediaPlayerStatus </th> 
   <th colname="col2" class="entry"> Se produce cuando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>La aplicación ha solicitado un reproductor multimedia nuevo llamando a <span class="codeph"> playerWithMediaPlayerItem</span>. El reproductor recién creado está esperando a que especifique un elemento del reproductor de contenidos. Este es el estado inicial del reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>La aplicación llama a <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>y se está cargando el reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK ha establecido correctamente el elemento del reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>El contenido se prepara y los anuncios se insertan en la cronología, o bien se produce un error en el procedimiento publicitario. Puede comenzar el almacenamiento en búfer o la reproducción. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>La aplicación ha llamado a <span class="codeph"> play</span>, por lo que TVSDK intenta reproducir el vídeo. Es posible que se produzca algún almacenamiento en búfer antes de que se reproduzca el vídeo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>A medida que la aplicación reproduce y pausa el contenido, el reproductor de contenido se mueve entre este estado y <span class="codeph"> PTMediaPlayerStatusPlaying</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>El reproductor ha llegado al final de la emisión y la reproducción se ha detenido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>La aplicación ha lanzado el reproductor multimedia, que también libera todos los recursos asociados. Ya no puede utilizar esta instancia </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>Se ha producido un error durante el proceso. Un error también puede afectar a lo que la aplicación puede hacer a continuación. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Puede utilizar el estado para proporcionar comentarios sobre el proceso (por ejemplo, un control de número mientras espera el siguiente cambio de estado) o para dar el siguiente paso en la reproducción del contenido, como esperar al estado adecuado antes de llamar al siguiente método.
