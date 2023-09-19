---
description: Desde el momento en que crea la instancia de MediaPlayer hasta el momento en que la finaliza (la reutiliza o la elimina), esta instancia completa una serie de transiciones entre estados.
title: Ciclo de vida del objeto MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Ciclo de vida del objeto MediaPlayer{#mediaplayer-object-lifecycle}

Desde el momento en que crea la instancia de MediaPlayer hasta el momento en que la finaliza (la reutiliza o la elimina), esta instancia completa una serie de transiciones entre estados.

Algunas operaciones solo se permiten cuando el reproductor está en un estado concreto. Por ejemplo, llamar a `play` in `IDLE` no está permitido. Solo puede invocar este estado una vez que el reproductor haya alcanzado el `PREPARED` estado.

Para trabajar con estados:

* Puede recuperar el estado actual del `MediaPlayer` objeto con `MediaPlayer.getStatus`.

  ```java
  PlayerState getStatus() throws IllegalStateException;
  ```

* La lista de estados se define en `MediaPlayer.PlayerState`.

Diagrama de transición de estados para el ciclo de vida de un `MediaPlayer` instancia:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

La siguiente tabla proporciona detalles adicionales:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> MediaPlayer.PlayerState </th> 
   <th colname="col2" class="entry"> Se produce cuando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INACTIVO </span> </td> 
   <td colname="col2"> <p>La aplicación ha solicitado un reproductor multimedia nuevo llamando a <span class="codeph"> DefaultMediaPlayer.create </span>. El reproductor recién creado está esperando a que especifique un elemento del reproductor de contenidos. Este es el estado inicial del reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZACIÓN </span> </td> 
   <td colname="col2"> <p>La aplicación ha llamado a <span class="codeph"> MediaPlayer.replaceCurrentItem </span>y se está cargando el reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZADO </span> </td> 
   <td colname="col2"> <p>TVSDK ha establecido correctamente el elemento del reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARANDO </span> </td> 
   <td colname="col2"> <p>La aplicación ha llamado a <span class="codeph"> MediaPlayer.prepareToPlay </span>. El reproductor de contenidos está cargando el elemento del reproductor de contenidos y los recursos asociados. </p> <p>Sugerencia: Es posible que se produzca algún almacenamiento en búfer de los medios principales. </p> <p>TVSDK está preparando el flujo de medios e intentando resolver e insertar anuncios (si está activado). </p> <p>Sugerencia: Para establecer la hora de inicio en un valor distinto de cero, llame a <span class="codeph"> prepareToPlay(startTime) </span> con el tiempo en milisegundos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARADO </span> </td> 
   <td colname="col2"> <p>El contenido se prepara y los anuncios se insertan en la cronología, o bien se produce un error en el procedimiento publicitario. Puede comenzar el almacenamiento en búfer o la reproducción. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> JUGANDO </span> </td> 
   <td colname="col2"> <p>La aplicación ha llamado a <span class="codeph"> play </span>, por lo que TVSDK intenta reproducir el vídeo. Es posible que se produzca algún almacenamiento en búfer antes de que se reproduzca el vídeo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PAUSADO </span> </td> 
   <td colname="col2"> <p>A medida que la aplicación reproduce y pausa el contenido, el reproductor de contenido se mueve entre este estado y REPRODUCIENDO. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> SUSPENDIDO </span> </td> 
   <td colname="col2"> <p>La aplicación salió de la reproducción, apagó el dispositivo o cambió de aplicación mientras el reproductor se estaba reproduciendo o pausó. El reproductor de contenidos se ha suspendido y se han liberado los recursos. Para continuar, restaure el reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> COMPLETADO </span> </td> 
   <td colname="col2"> <p>El reproductor ha llegado al final de la emisión y la reproducción se ha detenido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PUBLICADO </span> </td> 
   <td colname="col2"> <p>La aplicación ha lanzado el reproductor multimedia, que también libera todos los recursos asociados. Ya no puede utilizar esta instancia </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ERROR </span> </td> 
   <td colname="col2"> <p>Se ha producido un error durante el proceso. Un error también puede afectar a lo que la aplicación puede hacer a continuación. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Puede utilizar el estado para proporcionar comentarios sobre el proceso (por ejemplo, un control de número mientras espera el siguiente cambio de estado) o para dar el siguiente paso en la reproducción de medios, como esperar al estado adecuado antes de llamar al siguiente método.

Por ejemplo:

```java
@Override 
public void onStateChanged(MediaPlayer.PlayerState state,  
                           MediaPlayerNotification notification) { 
   switch (state) { 
      // It is recommended that you call prepareToPlay() after receiving  
      // the INITIALIZED state. 
      case INITIALIZED: 
         _mediaPlayer.prepareToPlay(); 
         break; 
      case PREPARING: 
         showBufferingSpinner(); 
         break; 
      case PREPARED: 
         hideBufferingSpinner(); 
      ..... 
    } 
}
```
