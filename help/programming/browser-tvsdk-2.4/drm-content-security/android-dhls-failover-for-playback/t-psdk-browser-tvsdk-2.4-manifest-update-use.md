---
description: Puede activar esta función y buscar eventos relacionados.
title: Usar actualización activa del manifiesto maestro
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Usar actualización activa del manifiesto maestro{#use-live-master-manifest-update}

Puede activar esta función y buscar eventos relacionados.

1. Para activar las actualizaciones del manifiesto principal activo, establezca la frecuencia de actualización (en minutos) configurando `NetworkConfiguration.masterUpdateInterval` propiedad.
1. De forma opcional, rastree las actualizaciones de manifiesto correctas escuchando el `MediaPlayerItemEvent.MASTER_UPDATED` evento.
