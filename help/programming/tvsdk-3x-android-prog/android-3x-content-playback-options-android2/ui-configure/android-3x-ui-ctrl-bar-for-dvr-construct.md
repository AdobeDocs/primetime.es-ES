---
description: Puede implementar una barra de control con soporte DVR para VOD y transmisión en vivo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.
title: Construya una barra de control mejorada para DVR
exl-id: 12e989f3-0e39-4224-89a7-ebfeb130f5fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# Construya una barra de control mejorada para DVR {#construct-a-control-bar-enhanced-for-dvr}

Puede implementar una barra de control con soporte DVR para VOD y transmisión en vivo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.

* Para VOD, la longitud de la ventana que se puede buscar es la duración de todo el recurso.
* Para la transmisión en directo, la longitud de la ventana DVR (buskable) se define como el intervalo de tiempo que comienza en la ventana de reproducción en directo y termina en el punto de activación del cliente.

   Recuerde la siguiente información:

   * El punto activo del cliente se calcula restando la longitud almacenada en el búfer del final de la ventana activa.

      La duración del objetivo es un valor mayor o igual que la duración máxima de un fragmento en el manifiesto.
   * El valor predeterminado es 10 000 ms.
   * La barra de control para la reproducción en directo admite DVR colocando primero el pulgar en el punto de lanzamiento del cliente al iniciar la reproducción y mostrando una región que marca el área donde no se permite la búsqueda.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. Para implementar una barra de control con soporte DVR, siga los pasos indicados en [Mostrar una barra de depuración con la posición de reproducción actual.](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md) con las siguientes diferencias:

   * Puede implementar una barra de control que esté asignada únicamente para el rango que se puede buscar, en lugar de para el rango de reproducción.

      Cualquier interacción del usuario para la búsqueda se puede considerar segura en el rango buscable.
   * Puede implementar una barra de control que esté asignada para el intervalo de reproducción, pero que también muestre el intervalo que se puede buscar.

      Para una barra de control:
   1. Agregue una superposición a la barra de control que represente el intervalo de reproducción.
   1. Cuando el usuario empiece a buscar, compruebe si la posición de búsqueda deseada se encuentra dentro del rango que se puede buscar utilizando `MediaPlayer.getSeekableRange`.

      Por ejemplo:

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      También puede optar por buscar en el punto activo del cliente utilizando la variable `MediaPlayer.LIVE_POINT` constante.

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
