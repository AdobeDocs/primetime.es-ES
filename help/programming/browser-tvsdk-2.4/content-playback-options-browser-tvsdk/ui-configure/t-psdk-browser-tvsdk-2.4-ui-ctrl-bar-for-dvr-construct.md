---
description: Puede implementar una barra de control con soporte DVR para VOD y transmisión en vivo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.
title: Construya una barra de control mejorada para DVR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Construya una barra de control mejorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

Puede implementar una barra de control con soporte DVR para VOD y transmisión en vivo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.

* Para VOD, la longitud de la ventana que se puede buscar es la duración de todo el recurso.
* Para la transmisión en directo, la longitud de la ventana DVR (buskable) se define como el intervalo de tiempo que comienza en la ventana de reproducción en directo y termina en el punto de activación del cliente.

   El punto activo del cliente se calcula restando la longitud almacenada en el búfer del final de la ventana activa. La duración del objetivo es un valor mayor o igual que la duración máxima de un fragmento en el manifiesto.

   La barra de control para la reproducción en directo admite DVR colocando primero el pulgar en el punto de lanzamiento del cliente al iniciar la reproducción y mostrando una región que marca el área donde no se permite la búsqueda.

Para una barra de control:

1. Agregue una superposición a la barra de control que represente el intervalo de reproducción.

1. Cuando el usuario empiece a buscar, compruebe si la posición de búsqueda deseada está dentro del rango en el que se puede buscar.
