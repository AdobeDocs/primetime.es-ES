---
description: Puede activar esta función y comprobar si hay eventos relacionados.
seo-description: Puede activar esta función y comprobar si hay eventos relacionados.
seo-title: Usar actualización de maestro-manifiesto en directo
title: Usar actualización de maestro-manifiesto en directo
uuid: 4ec665ab-b7ce-4a45-a251-13a07eb4d789
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Usar actualización de maestro-manifiesto en directo{#use-live-master-manifest-update}

Puede activar esta función y comprobar si hay eventos relacionados.

1. Para activar las actualizaciones de manifiesto maestro en vivo, establezca la frecuencia de actualización (en minutos) estableciendo la `NetworkConfiguration.masterUpdateInterval` propiedad.
1. De forma opcional, rastree las actualizaciones de manifiesto correctas escuchando el `MediaPlayerItemEvent.MASTER_UPDATED` evento.
