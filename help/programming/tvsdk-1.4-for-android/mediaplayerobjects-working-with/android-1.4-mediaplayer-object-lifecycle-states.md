---
description: Desde el momento en que crea la instancia de MediaPlayer hasta el momento en que la cierra (vuelve a utilizar o elimina), esta instancia completa una serie de transiciones entre estados.
title: Ciclo de vida del objeto MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Ciclo de vida del objeto MediaPlayer{#mediaplayer-object-lifecycle}

Desde el momento en que crea la instancia de MediaPlayer hasta el momento en que la cierra (vuelve a utilizar o elimina), esta instancia completa una serie de transiciones entre estados.

Algunas operaciones solo se permiten cuando el reproductor está en un estado concreto. Por ejemplo, no se permite llamar a `play` en `IDLE`. Puede llamar a este estado solo después de que el reproductor alcance el estado `PREPARED` .

Para trabajar con estados:

* Puede recuperar el estado actual del objeto `MediaPlayer` con `MediaPlayer.getStatus`.

   ```java
   PlayerState getStatus() throws IllegalStateException;
   ```

* La lista de estados se define en `MediaPlayer.PlayerState`.

Diagrama de transición de estado para el ciclo vital de una instancia `MediaPlayer`:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

En la tabla siguiente se proporcionan detalles adicionales:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> MediaPlayer.PlayerState </th> 
   <th colname="col2" class="entry"> Ocurre cuando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> IDLE  </span> </td> 
   <td colname="col2"> <p>La aplicación solicitó un nuevo reproductor de contenidos llamando a <span class="codeph"> DefaultMediaPlayer.create </span>. El reproductor recién creado está esperando a que especifique un elemento del reproductor de contenidos. Este es el estado inicial del reproductor de medios. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZACIÓN  </span> </td> 
   <td colname="col2"> <p>La aplicación denominada <span class="codeph"> MediaPlayer.replaceCurrentItem </span> y se está cargando el reproductor de medios. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZADO  </span> </td> 
   <td colname="col2"> <p>TVSDK estableció correctamente el elemento del reproductor de medios. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARACIÓN  </span> </td> 
   <td colname="col2"> <p>La aplicación se llama <span class="codeph"> MediaPlayer.prepareToPlay </span>. El reproductor de contenidos está cargando el elemento del reproductor de contenidos y los recursos asociados. </p> <p>Sugerencia:  Puede que se produzca algún almacenamiento en búfer del contenido principal. </p> <p>TVSDK está preparando el flujo de medios e intentando realizar la resolución de anuncios y la inserción de anuncios, (si está habilitada). </p> <p>Sugerencia:  Para establecer el tiempo de inicio en un valor distinto de cero, llame a <span class="codeph"> prepareToPlay(startTime) </span> con el tiempo en milisegundos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARADO  </span> </td> 
   <td colname="col2"> <p>El contenido está preparado y se han insertado anuncios en la cronología, o el procedimiento de publicidad ha fallado. Puede comenzar el almacenamiento en búfer o la reproducción. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> REPRODUCCIÓN  </span> </td> 
   <td colname="col2"> <p>La aplicación ha llamado <span class="codeph"> play </span>, por lo que TVSDK está intentando reproducir el vídeo. Puede que se produzca algún almacenamiento en búfer antes de que se reproduzca realmente el vídeo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> EN PAUSA  </span> </td> 
   <td colname="col2"> <p>A medida que la aplicación reproduce y pone en pausa el contenido, el reproductor de contenidos se mueve entre este estado y REPRODUCIENDO. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> SUSPENDIDO  </span> </td> 
   <td colname="col2"> <p>La aplicación se alejó de la reproducción, apagó el dispositivo o cambió de aplicación mientras el reproductor se estaba reproduciendo o pausando. Se ha suspendido el reproductor de contenidos y se han liberado recursos. Para continuar, restaure el reproductor multimedia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> COMPLETAR  </span> </td> 
   <td colname="col2"> <p>El reproductor ha llegado al final de la emisión y la reproducción se ha detenido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PUBLICADO  </span> </td> 
   <td colname="col2"> <p>La aplicación ha lanzado el reproductor de contenido, que también libera todos los recursos asociados. Ya no se puede usar esta instancia </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ERROR  </span> </td> 
   <td colname="col2"> <p>Error durante el proceso. Un error también podría afectar a lo que puede hacer la aplicación a continuación. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Puede utilizar el estado para proporcionar comentarios sobre el proceso (por ejemplo, un control de número mientras espera el siguiente cambio de estado) o para dar el siguiente paso en la reproducción del contenido, como esperar al estado adecuado antes de llamar al siguiente método.

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

