---
description: La propiedad MediaPlayerItem.timedMetadata proporciona acceso a todos los objetos TimedMetadata que se crean a partir de etiquetas playlist/manifest o de etiquetas ID3 en el flujo de medios.
seo-description: La propiedad MediaPlayerItem.timedMetadata proporciona acceso a todos los objetos TimedMetadata que se crean a partir de etiquetas playlist/manifest o de etiquetas ID3 en el flujo de medios.
seo-title: Notificaciones para etiquetas de manifiesto
title: Notificaciones para etiquetas de manifiesto
uuid: 50727455-b37b-4e39-8efb-a97de3164074
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Notificaciones para etiquetas de manifiesto{#notifications-for-manifest-tags}

La propiedad MediaPlayerItem.timedMetadata proporciona acceso a todos los objetos TimedMetadata que se crean a partir de etiquetas playlist/manifest o de etiquetas ID3 en el flujo de medios.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

La propiedad `MediaPlayerItem.hasTimedMetadata` indica si existe una etiqueta personalizada suscrita en el medio actual. Puede monitorear los metadatos temporizados escuchando el `Events.TimedMetadataEvent`, que la instancia de MediaPlayer distribuye cada vez que se crea un nuevo objeto `TimedMetadata`.
