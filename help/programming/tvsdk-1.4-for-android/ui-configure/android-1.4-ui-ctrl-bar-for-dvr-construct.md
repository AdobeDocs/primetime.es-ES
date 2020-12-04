---
description: Puede implementar una barra de control con compatibilidad con DVR para VOD y transmisión en directo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.
seo-description: Puede implementar una barra de control con compatibilidad con DVR para VOD y transmisión en directo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.
seo-title: Construir una barra de control mejorada para DVR
title: Construir una barra de control mejorada para DVR
uuid: c9c86383-379f-452c-b35d-447ac8691fa0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---


# Construir una barra de control mejorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

Puede implementar una barra de control con compatibilidad con DVR para VOD y transmisión en directo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.

* Para VOD, la longitud de la ventana que se puede buscar es la duración de todo el recurso.
* Para la transmisión en directo, la duración de la ventana DVR (buskable) se define como el intervalo de tiempo que comienza en la ventana de reproducción en directo y termina en el punto de activación del cliente.

   El punto activo del cliente se calcula restando la longitud almacenada en el búfer del extremo de la ventana activa. La duración del destinatario es un valor mayor o igual que la duración máxima de un fragmento en el manifiesto.

   El valor predeterminado es 10000 ms.

   La barra de control para la reproducción en directo admite DVR colocando primero el pulgar en el punto activo del cliente al iniciar la reproducción y mostrando una región que marca el área en la que no se permite la búsqueda.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. Para implementar una barra de control con compatibilidad con DVR, siga los pasos para mostrar una barra de búsqueda, con algunas diferencias menores:

   * Puede elegir implementar una barra de control que se asigne solamente para el rango buscable en lugar de para el rango de reproducción. Cualquier interacción del usuario para la búsqueda puede considerarse segura en el rango buscable.
   * Puede elegir implementar una barra de control que esté asignada para el rango de reproducción pero que también muestre el rango que se puede buscar.

      Para una barra de control:
   1. Añada una superposición en la barra de control que representa el rango de reproducción.
   1. Cuando el usuario inicio buscar, compruebe si la posición de búsqueda deseada se encuentra dentro del rango buscable mediante `MediaPlayer.getSeekableRange`.

      Por ejemplo:

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      También puede optar por buscar en el punto activo del cliente mediante la constante `MediaPlayer.LIVE_POINT`.

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
