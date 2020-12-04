---
description: El objeto PTMediaPlayer representa el reproductor multimedia. Un PTMediaPlayerItem representa audio o vídeo en el reproductor.
seo-description: El objeto PTMediaPlayer representa el reproductor multimedia. Un PTMediaPlayerItem representa audio o vídeo en el reproductor.
seo-title: Trabajo con objetos de MediaPlayer
title: Trabajo con objetos de MediaPlayer
uuid: 0c33ebd6-b11a-4e62-8c1c-880cfceff474
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---


# Trabajo con objetos de MediaPlayer {#work-with-mediaplayer-objects}

El objeto PTMediaPlayer representa el reproductor multimedia. Un PTMediaPlayerItem representa audio o vídeo en el reproductor.

## Acerca de la clase MediaPlayerItem {#section_B6F36C0462644F5C932C8AA2F6827071}

Después de cargar correctamente un recurso multimedia, TVSDK crea una instancia de la clase `PTMediaPlayerItem` para proporcionar acceso a ese recurso.

El `PTMediaPlayer` resuelve el recurso de medios, carga el archivo de manifiesto asociado y analiza el manifiesto. Es la parte asincrónica del proceso de carga de recursos. La instancia `PTMediaPlayerItem` se produce una vez resuelto el recurso y esta instancia es una versión resuelta de un recurso de medios. TVSDK proporciona acceso a la instancia `PTMediaPlayerItem` recién creada mediante `PTMediaPlayer.currentItem`.

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor multimedia.

## Ciclo de vida del objeto MediaPlayer {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

Desde el momento en que se crea la instancia `PTMediaPlayer` hasta el momento en que se termina (se vuelve a utilizar o se elimina), esta instancia completa una serie de transiciones de un estado a otro.

Algunas operaciones solo se permiten cuando el reproductor se encuentra en un estado concreto. Por ejemplo, no se permite llamar a `play` en `PTMediaPlayerStatusCreated`. Sólo puede llamar a este estado después de que el reproductor alcance el estado `PTMediaPlayerStatusReady`.

Para trabajar con estados:

* Puede recuperar el estado actual del objeto MediaPlayer con `PTMediaPlayer.status`.
* La lista de los estados se define en `PTMediaPlayerStatus`.

Diagrama de estado-transición para el ciclo vital de una instancia de MediaPlayer:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

En la tabla siguiente se proporcionan detalles adicionales:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>PTMediaPlayerStatus</b></th> 
   <th colname="col2" class="entry"><b>Ocurre cuando</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatuscreated</span> </p> </td> 
   <td colname="col2"> <p>La aplicación solicitó un nuevo reproductor de medios llamando a <span class="codeph"> playerWithMediaPlayerItem</span>. El reproductor recién creado está esperando a que especifique un elemento de reproductor de medios. Este es el estado inicial del reproductor de medios. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>La aplicación llama a <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span> y se está cargando el reproductor multimedia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK definió correctamente el elemento del reproductor de medios. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>El contenido se prepara y las publicidades se insertan en la línea de tiempo, o bien se produce un error en el procedimiento de publicidad. Puede comenzar la reproducción o el almacenamiento en búfer. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>La aplicación ha llamado a <span class="codeph"> play</span>, por lo que TVSDK está intentando reproducir el vídeo. Es posible que se produzca algún almacenamiento en búfer antes de que se reproduzca realmente el vídeo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>A medida que la aplicación reproduce y pausa el medio, el reproductor de medios se mueve entre este estado y <span class="codeph"> PTMediaPlayerStatusPlaying</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>El reproductor llegó al final del flujo y la reproducción se detuvo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>La aplicación ha lanzado el reproductor de medios, que también libera los recursos asociados. Ya no se puede usar esta instancia </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>Error durante el proceso. Un error también puede afectar a lo que la aplicación puede hacer a continuación. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Puede utilizar el estado para proporcionar comentarios sobre el proceso (por ejemplo, un control giratorio mientras espera el siguiente cambio de estado) o para dar el siguiente paso en la reproducción de los medios, como esperar al estado adecuado antes de llamar al siguiente método.