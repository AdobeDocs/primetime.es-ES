---
description: El estado del reproductor de contenidos determina qué acciones son legales.
title: Ciclo de vida y estados del objeto MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---


# Ciclo de vida y estados del objeto MediaPlayer{#lifecycle-and-statuses-of-the-mediaplayer-object}

El estado del reproductor de contenidos determina qué acciones son legales.

Para trabajar con estados del reproductor de medios:

* Puede recuperar el estado actual del objeto `MediaPlayer` con `MediaPlayer.getStatus()`.

* La lista de estados se define en la enumeración [MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/com/adobe/mediacore/MediaPlayerStatus.html).

Diagrama de estado-transición para el ciclo de vida de una instancia `MediaPlayer`:

<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

La siguiente tabla proporciona detalles sobre el ciclo de vida y los estados del reproductor de contenidos:

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estado </th> 
   <th colname="col2" class="entry"> Ocurre cuando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> IDLE </td> 
   <td colname="col2"> <p>Estado inicial del reproductor de contenidos. El reproductor se crea y está esperando a que especifique un elemento del reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INICIALIZACIÓN </td> 
   <td colname="col2"> <p>La aplicación llama a <span class="codeph"> MediaPlayer.replaceCurrentItem() </span>. </p> <p>Se está cargando el elemento del reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INICIALIZADO </td> 
   <td colname="col2"> <p>TVSDK estableció correctamente el elemento de reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARACIÓN </td> 
   <td colname="col2"> <p>La aplicación llama a <span class="codeph"> MediaPlayer.prepareToPlay() </span>. El reproductor de medios está cargando el elemento del reproductor de medios y los recursos asociados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARADO </td> 
   <td colname="col2"> <p>TVSDK ha preparado el flujo de medios y ha intentado realizar la resolución de anuncios y la inserción de anuncios (si está habilitada). El contenido está preparado y se han insertado anuncios en la cronología, o el procedimiento de publicidad ha fallado. </p> <p>Puede comenzar el almacenamiento en búfer o la reproducción. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> REPRODUCIR/PAUSAR </td> 
   <td colname="col2"> <p>A medida que la aplicación reproduce y pone en pausa el contenido, el reproductor de contenidos se mueve entre estos estados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> SUSPENDIDO </td> 
   <td colname="col2"> <p>Si la aplicación sale de la reproducción, apaga el dispositivo o cambia de aplicación mientras el reproductor se está reproduciendo o pausando, el reproductor de contenidos se suspende y se liberan los recursos. </p> <p>Llamar a <span class="codeph"> MediaPlayer.restore() </span> devuelve el reproductor al estado en el que se encontraba antes de SUSPENDER. La excepción es que si el reproductor está BUSCANDO cuando se llama a suspendido, el reproductor se PONE EN PAUSA y, a continuación, se SUSPENDE. </p> <p>Importante:  <p>Recuerde la siguiente información: 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">El <span class="codeph"> MediaPlayer </span> llama automáticamente a <span class="codeph"> suspender </span> solo cuando se destruye el objeto de superficie que utiliza el <span class="codeph"> MediaPlayerView </span>. </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">El <span class="codeph"> MediaPlayer </span> llama automáticamente a <span class="codeph"> restore() </span> solo cuando se crea un nuevo objeto de superficie que utiliza el <span class="codeph"> MediaPlayerView </span>. </li> 
      </ul> </p> </p> <p>Si siempre desea pausar la reproducción cuando se restaure MediaPlayer, pida a la aplicación que llame a <span class="codeph"> MediaPlayer.pause() </span> en el método <span class="codeph"> onPause() </span> de la actividad de Android. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> COMPLETAR </td> 
   <td colname="col2"> <p>El reproductor ha llegado al final de la emisión y la reproducción se ha detenido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PUBLICADO </td> 
   <td colname="col2"> <p>La aplicación ha lanzado el reproductor de contenido, que también libera todos los recursos asociados. Ya no puede utilizar esta instancia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ERROR </td> 
   <td colname="col2"> <p>Error durante el proceso. Un error también podría afectar a lo que la aplicación puede hacer a continuación. Para obtener más información, consulte <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-error-handling-set-up.md" format="dita" scope="local"> Configuración de la gestión de errores </a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Puede utilizar el estado para proporcionar comentarios sobre el proceso, por ejemplo, un control de número mientras espera el siguiente cambio de estado, o seguir los siguientes pasos en la reproducción del contenido, como esperar al estado adecuado antes de llamar al siguiente método.

Por ejemplo:

```java
mediaPlayer.addEventListener(MediaPlayerEvent STATUS_CHANGED, new StatusChangeEventListener() { 
    @Override  
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        switch(event.getStatus()) { 
            case INITIALIZED: 
                mediaPlayer.prepareToPlay(); 
                break; 
            case PREPARING: 
                showBufferingSpinner(); 
                break; 
            case PREPARED: 
                hideBufferingSpinner(); 
                mediaPlayer.play(); 
                break; 
            ...                
        } 
        ... 
    } 
}); 
```
