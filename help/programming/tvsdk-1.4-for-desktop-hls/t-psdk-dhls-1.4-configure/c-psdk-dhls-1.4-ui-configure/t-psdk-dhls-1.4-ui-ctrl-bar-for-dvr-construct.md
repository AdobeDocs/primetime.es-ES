---
description: Puede implementar una barra de control con compatibilidad con DVR para VOD y transmisión en directo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.
seo-description: Puede implementar una barra de control con compatibilidad con DVR para VOD y transmisión en directo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.
seo-title: Construir una barra de control mejorada para DVR
title: Construir una barra de control mejorada para DVR
uuid: 08f943e8-90da-4860-92dd-dd289fd68cba
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Construir una barra de control mejorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

Puede implementar una barra de control con compatibilidad con DVR para VOD y transmisión en directo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.

* Para VOD, la longitud de la ventana que se puede buscar es la duración de todo el recurso.
* Para la transmisión en directo, la duración de la ventana DVR (buskable) se define como el intervalo de tiempo que comienza en la ventana de reproducción en directo y termina en el punto de activación del cliente.

   El punto activo del cliente se calcula restando la longitud almacenada en el búfer del extremo de la ventana activa. La duración de destino es un valor mayor o igual que la duración máxima de un fragmento en el manifiesto.

   El valor predeterminado es 10000 ms.

   La barra de control para la reproducción en directo admite DVR colocando primero el pulgar en el punto activo del cliente al iniciar la reproducción y mostrando una región que marca el área en la que no se permite la búsqueda.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. Para implementar una barra de control con compatibilidad con DVR, siga los pasos para mostrar una barra de búsqueda, con algunas diferencias menores:

   * Puede elegir implementar una barra de control que se asigne solamente para el rango buscable en lugar de para el rango de reproducción. Cualquier interacción del usuario para la búsqueda puede considerarse segura en el rango buscable.
   * Puede elegir implementar una barra de control que esté asignada para el rango de reproducción pero que también muestre el rango que se puede buscar.

      Para una barra de control:
   1. Agregue una superposición a la barra de control que represente el rango de reproducción.
   1. Cuando el usuario comienza a buscar, compruebe si la posición de búsqueda deseada se encuentra dentro del rango que se puede buscar mediante la `MediaPlayer.seekableRange` propiedad .

      Por ejemplo:

      ```
      var desiredPosition:Number = // TODO : choose a value 
      
      private function onStatusChange(event:MediaPlayerStatusChangeEvent):void { 
          switch(event.status) { 
              case MediaPlayerStatus.PREPARED: 
                  _mediaPlayer.prepareToPlay(desiredPosition); 
          } 
      }
      ```

      También puede optar por buscar en el punto activo del cliente mediante la `MediaPlayer.LIVE_POINT` constante.

      ```
      private function onSeekToLiveClick(event:MouseEvent):void { 
          _player.seek(DefaultMediaPlayer.LIVE_POINT); 
      }
      ```


