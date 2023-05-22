---
description: Puede implementar una barra de control compatible con DVR para VOD y streaming en vivo. La compatibilidad con DVR incluye el concepto de una ventana en la que se puede buscar y el punto de activación del cliente.
title: Construir una barra de control mejorada para DVR
exl-id: e4846f1e-bc57-452b-b393-8f8f55434e7a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Construir una barra de control mejorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

Puede implementar una barra de control compatible con DVR para VOD y streaming en vivo. La compatibilidad con DVR incluye el concepto de una ventana en la que se puede buscar y el punto de activación del cliente.

* En el caso de VOD, la duración de la ventana en la que se puede buscar es la duración de todo el recurso.
* Para el streaming en directo, la duración de la ventana del DVR (seleccionable) se define como el intervalo de tiempo que comienza en la ventana de reproducción en directo y termina en el punto en directo del cliente.

   El punto activo del cliente se calcula restando la longitud almacenada en búfer del final de la ventana activa. La duración de destino es un valor mayor o igual que la duración máxima de un fragmento en el manifiesto.

   La barra de control para la reproducción en directo admite DVR colocando primero el pulgar en el punto de reproducción en directo del cliente al iniciar la reproducción y mostrando una región que marca el área donde no se permite la búsqueda.

Para una barra de control:

1. Agregue una superposición a la barra de control que represente el intervalo de reproducción.

1. Cuando el usuario empieza a buscar, comprueba si la posición de búsqueda deseada está dentro del rango de búsqueda.
