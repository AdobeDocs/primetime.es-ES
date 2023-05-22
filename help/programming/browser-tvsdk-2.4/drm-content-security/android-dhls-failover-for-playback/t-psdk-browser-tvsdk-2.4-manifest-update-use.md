---
description: Puede activar esta función y buscar eventos relacionados.
title: Usar actualización activa del manifiesto maestro
exl-id: 02cb3116-cc30-4139-841b-8d6297214b8b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Usar actualización activa del manifiesto maestro{#use-live-master-manifest-update}

Puede activar esta función y buscar eventos relacionados.

1. Para activar las actualizaciones del manifiesto principal activo, establezca la frecuencia de actualización (en minutos) configurando `NetworkConfiguration.masterUpdateInterval` propiedad.
1. De forma opcional, rastree las actualizaciones de manifiesto correctas escuchando el `MediaPlayerItemEvent.MASTER_UPDATED` evento.
