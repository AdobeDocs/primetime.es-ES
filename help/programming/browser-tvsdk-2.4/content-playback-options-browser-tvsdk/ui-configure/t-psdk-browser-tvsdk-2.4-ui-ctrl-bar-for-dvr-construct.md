---
description: Puede implementar una barra de control con compatibilidad con DVR para VOD y transmisión en directo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.
seo-description: Puede implementar una barra de control con compatibilidad con DVR para VOD y transmisión en directo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.
seo-title: Construir una barra de control mejorada para DVR
title: Construir una barra de control mejorada para DVR
uuid: 83c56def-a454-4f26-bdfc-2ef2497ef9bd
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Construir una barra de control mejorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

Puede implementar una barra de control con compatibilidad con DVR para VOD y transmisión en directo. La compatibilidad con DVR incluye el concepto de una ventana que se puede buscar y el punto activo del cliente.

* Para VOD, la longitud de la ventana que se puede buscar es la duración de todo el recurso.
* Para la transmisión en directo, la duración de la ventana DVR (buskable) se define como el intervalo de tiempo que comienza en la ventana de reproducción en directo y termina en el punto de activación del cliente.

   El punto activo del cliente se calcula restando la longitud almacenada en el búfer del extremo de la ventana activa. La duración de destino es un valor mayor o igual que la duración máxima de un fragmento en el manifiesto.

   La barra de control para la reproducción en directo admite DVR colocando primero el pulgar en el punto activo del cliente al iniciar la reproducción y mostrando una región que marca el área en la que no se permite la búsqueda.

Para una barra de control:

1. Agregue una superposición a la barra de control que represente el rango de reproducción.

1. Cuando el usuario comienza a buscar, compruebe si la posición deseada de la búsqueda se encuentra dentro del rango buscable.
