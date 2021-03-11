---
description: Puede activar esta función y comprobar si hay eventos relacionados.
title: Usar actualización de manifiesto maestro en vivo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---


# Usar actualización de manifiesto maestro en vivo{#use-live-master-manifest-update}

Puede activar esta función y comprobar si hay eventos relacionados.

1. Para activar las actualizaciones de manifiesto maestro en vivo, establezca la frecuencia de actualización (en minutos) estableciendo la propiedad `NetworkConfiguration.masterUpdateInterval`.
1. Opcionalmente, puede rastrear las actualizaciones de manifiesto correctas escuchando el evento `MediaPlayerItemEvent.MASTER_UPDATED`.
