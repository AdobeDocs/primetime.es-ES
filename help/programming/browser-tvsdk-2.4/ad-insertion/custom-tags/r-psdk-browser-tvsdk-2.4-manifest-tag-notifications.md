---
description: La propiedad MediaPlayerItem.timedMetadata proporciona acceso a todos los objetos TimedMetadata creados a partir de etiquetas de lista de reproducción/manifiesto o a partir de etiquetas ID3 en el flujo de medios.
title: Notificaciones para etiquetas de manifiesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Notificaciones para etiquetas de manifiesto{#notifications-for-manifest-tags}

La propiedad MediaPlayerItem.timedMetadata proporciona acceso a todos los objetos TimedMetadata creados a partir de etiquetas de lista de reproducción/manifiesto o a partir de etiquetas ID3 en el flujo de medios.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

La propiedad `MediaPlayerItem.hasTimedMetadata` indica si existe una etiqueta personalizada suscrita en el medio actual. Puede monitorizar los metadatos temporizados escuchando el `Events.TimedMetadataEvent`, que la instancia de MediaPlayer distribuye cada vez que se crea un nuevo objeto `TimedMetadata`.
