---
description: Puede implementar una barra de control compatible con DVR para VOD y streaming en vivo. La compatibilidad con DVR incluye el concepto de una ventana en la que se puede buscar y el punto de activación del cliente.
title: Construir una barra de control mejorada para DVR
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Construir una barra de control mejorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

Puede implementar una barra de control compatible con DVR para VOD y streaming en vivo. La compatibilidad con DVR incluye el concepto de una ventana en la que se puede buscar y el punto de activación del cliente.

* En el caso de VOD, la duración de la ventana en la que se puede buscar es la duración de todo el recurso.
* Para el streaming en directo, la duración de la ventana del DVR (seleccionable) se define como el intervalo de tiempo que comienza en la ventana de reproducción en directo y termina en el punto en directo del cliente.

  El punto activo del cliente se calcula restando la longitud almacenada en búfer del final de la ventana activa. La duración de destino es un valor mayor o igual que la duración máxima de un fragmento en el manifiesto.

  El valor predeterminado es 10000 ms.

  La barra de control para la reproducción en directo admite DVR colocando primero el pulgar en el punto de reproducción en directo del cliente al iniciar la reproducción y mostrando una región que marca el área donde no se permite la búsqueda.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. Para implementar una barra de control compatible con DVR, siga los pasos para mostrar una barra de desplazamiento de búsqueda, con algunas diferencias menores:

   * Puede elegir implementar una barra de control que esté asignada únicamente para el rango buscable en lugar de para el rango de reproducción. Cualquier interacción del usuario para seek puede considerarse segura dentro del rango buscable.
   * Puede elegir implementar una barra de control asignada para el rango de reproducción, pero que también muestre el rango buscable.

     Para una barra de control:

   1. Agregue una superposición a la barra de control que represente el intervalo de reproducción.
   1. Cuando el usuario empieza a buscar, compruebe si la posición de búsqueda deseada está dentro del rango de búsqueda mediante `MediaPlayer.getSeekableRange`.

      Por ejemplo:

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      También puede elegir buscar en el punto activo del cliente mediante la variable `MediaPlayer.LIVE_POINT` constante.

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
