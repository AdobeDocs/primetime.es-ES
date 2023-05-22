---
description: El estado del reproductor de contenidos determina qué acciones son legales.
title: Ciclo de vida y estados del objeto MediaPlayer
exl-id: 6b43f334-bd21-4d0e-a123-fd99403a6082
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Ciclo de vida y estados del objeto MediaPlayer {#lifecycle-and-statuses-of-the-mediaplayer-object}

El estado del reproductor de contenidos determina qué acciones son legales.

Para trabajar con estados de reproductor de contenidos:

* Puede recuperar el estado actual de `MediaPlayer` objeto con `MediaPlayer.getStatus()`.

* La lista de estados se define en la variable [MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/com/adobe/mediacore/MediaPlayerStatus.html) enum.

Diagrama de transición de estado para el ciclo de vida de un `MediaPlayer` instancia:
<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

La siguiente tabla proporciona detalles sobre el ciclo de vida y los estados del reproductor de contenidos:

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Estado </th> 
   <th colname="col2" class="entry"> Se produce cuando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> INACTIVO </td> 
   <td colname="col2"> <p>Estado inicial del reproductor de contenido. El reproductor se crea y está esperando a que especifique un elemento del reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INICIALIZACIÓN </td> 
   <td colname="col2"> <p>La aplicación llama a <span class="codeph"> MediaPlayer.replaceCurrentItem() </span>. </p> <p>Se está cargando el elemento del reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INICIALIZADO </td> 
   <td colname="col2"> <p>TVSDK ha establecido correctamente el elemento del reproductor de contenidos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARANDO </td> 
   <td colname="col2"> <p>La aplicación llama a <span class="codeph"> MediaPlayer.prepareToPlay() </span>. El reproductor de contenidos está cargando el elemento del reproductor de contenidos y los recursos asociados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARADO </td> 
   <td colname="col2"> <p>TVSDK ha preparado el flujo de medios y ha intentado realizar la resolución de anuncios y la inserción de anuncios (si está activada). El contenido se prepara y los anuncios se insertan en la cronología, o bien se produce un error en el procedimiento publicitario. </p> <p>Puede comenzar el almacenamiento en búfer o la reproducción. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> REPRODUCCIÓN/PAUSA </td> 
   <td colname="col2"> <p>A medida que la aplicación reproduce y pausa el contenido, el reproductor de contenido se mueve entre estos estados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> SUSPENDIDO </td> 
   <td colname="col2"> <p>Si la aplicación sale de la reproducción, apaga el dispositivo o cambia de aplicación mientras el reproductor se está reproduciendo o pausando, el reproductor de contenidos se suspende y se liberan los recursos. </p> <p>Llamando <span class="codeph"> MediaPlayer.restore() </span> devuelve al reproductor al estado en el que se encontraba antes de SUSPENDERLO. La excepción es que si se llama al reproductor SEEKING cuando está suspendido, el reproductor se PONE EN PAUSA y luego SE SUSPENDE. </p> <p>Importante:  <p>Recuerde la siguiente información: 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">El <span class="codeph"> MediaPlayer </span> llama automáticamente a <span class="codeph"> suspender </span> sólo cuando el objeto de superficie utilizado por <span class="codeph"> MediaPlayerView </span> se destruye. </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">El <span class="codeph"> MediaPlayer </span> llama automáticamente a <span class="codeph"> restore() </span> sólo cuando se utiliza un objeto de superficie nuevo por la variable <span class="codeph"> MediaPlayerView </span> se ha creado. </li> 
      </ul> </p> </p> <p>Si siempre desea que la reproducción se detenga cuando se restaure MediaPlayer, solicite a la aplicación que invoque <span class="codeph"> MediaPlayer.pause() </span> en la actividad de Android <span class="codeph"> onPause() </span> método. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> COMPLETADO </td> 
   <td colname="col2"> <p>El reproductor ha llegado al final del flujo y la reproducción se ha detenido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PUBLICADO </td> 
   <td colname="col2"> <p>La aplicación ha lanzado el reproductor de contenidos, que también libera todos los recursos asociados. Ya no puede utilizar esta instancia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ERROR </td> 
   <td colname="col2"> <p>Se ha producido un error durante el proceso. Un error también puede afectar a lo que la aplicación puede hacer a continuación. Para obtener más información, consulte <a href="../../../tvsdk-2.7-for-android/content-playback-options/t-psdk-android-2.7-error-handling-set-up.md#set-up-error-handling" format="dita" scope="local"> Configuración de la gestión de errores </a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Puede utilizar el estado para proporcionar comentarios sobre el proceso, por ejemplo, un control de número mientras espera el siguiente cambio de estado, o realizar los siguientes pasos en la reproducción de medios, como esperar el estado adecuado antes de llamar al siguiente método.

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
