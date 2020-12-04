---
description: Puede activar esta función y comprobar si hay eventos relacionados.
seo-description: Puede activar esta función y comprobar si hay eventos relacionados.
seo-title: Usar actualización de maestro-manifiesto en directo
title: Usar actualización de maestro-manifiesto en directo
uuid: 4ec665ab-b7ce-4a45-a251-13a07eb4d789
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Usar actualización de maestro-manifiesto en directo{#use-live-master-manifest-update}

Puede activar esta función y comprobar si hay eventos relacionados.

1. Para activar las actualizaciones de master-manifest activas, establezca la frecuencia de actualización (en minutos) estableciendo la propiedad `NetworkConfiguration.masterUpdateInterval`.
1. Opcionalmente, rastree las actualizaciones de manifiesto correctas escuchando el evento `MediaPlayerItemEvent.MASTER_UPDATED`.
