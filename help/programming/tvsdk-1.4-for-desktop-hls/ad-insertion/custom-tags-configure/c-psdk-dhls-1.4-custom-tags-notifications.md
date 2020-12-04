---
description: La propiedad MediaPlayerItem.timedMetadata le permite acceder a todos los objetos TimedMetadata creados a partir de etiquetas playlist/manifest o a partir de etiquetas ID3 dentro del flujo de medios. La propiedad MediaPlayerItem.hasTimedMetadata indica si hay una etiqueta personalizada suscrita en el medio actual.
seo-description: La propiedad MediaPlayerItem.timedMetadata le permite acceder a todos los objetos TimedMetadata creados a partir de etiquetas playlist/manifest o a partir de etiquetas ID3 dentro del flujo de medios. La propiedad MediaPlayerItem.hasTimedMetadata indica si hay una etiqueta personalizada suscrita en el medio actual.
seo-title: Notificaciones para etiquetas de manifiesto
title: Notificaciones para etiquetas de manifiesto
uuid: 87bee41b-b44e-4d12-afd2-7a63023f992c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Notificaciones para etiquetas de manifiesto{#notifications-for-manifest-tags}

La propiedad MediaPlayerItem.timedMetadata le permite acceder a todos los objetos TimedMetadata creados a partir de etiquetas playlist/manifest o a partir de etiquetas ID3 dentro del flujo de medios. La propiedad MediaPlayerItem.hasTimedMetadata indica si hay una etiqueta personalizada suscrita en el medio actual.

Puede supervisar los metadatos temporizados escuchando los siguientes eventos, que notifican a la aplicación la actividad relacionada:

* `MediaPlayerItemEvent.ITEM_CREATED`:: La lista inicial de  `TimedMetadata` los objetos está disponible después de  `MediaPlayerItem` crearla. Este evento notifica a la aplicación cuando esto sucede.

* `MediaPlayerItemEvent.ITEM_UPDATED`:: En el caso de flujos en directo/lineales en los que el manifiesto/lista de reproducción se actualiza periódicamente, es posible que aparezcan etiquetas personalizadas adicionales en la lista de reproducción/manifiesto actualizado, por lo que se pueden agregar objetos TimedMetadata adicionales a la  `MediaPlayerItem.timedMetadata` propiedad. Este evento notifica a la aplicación cuando esto sucede.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`:: Cada vez que se crea un nuevo  `TimedMetadata` objeto, el  `MediaPlayer`usuario envía este evento. Este evento no se distribuye para el objeto `TimedMetadata` creado durante la fase de inicialización.

