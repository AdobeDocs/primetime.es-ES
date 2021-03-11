---
description: La propiedad MediaPlayerItem.timedMetadata le permite acceder a todos los objetos TimedMetadata creados a partir de etiquetas playlist/manifest o a partir de etiquetas ID3 en el flujo de medios. La propiedad MediaPlayerItem.hasTimedMetadata indica si existe una etiqueta personalizada suscrita en el medio actual.
title: Notificaciones para etiquetas de manifiesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Notificaciones para etiquetas de manifiesto{#notifications-for-manifest-tags}

La propiedad MediaPlayerItem.timedMetadata le permite acceder a todos los objetos TimedMetadata creados a partir de etiquetas playlist/manifest o a partir de etiquetas ID3 en el flujo de medios. La propiedad MediaPlayerItem.hasTimedMetadata indica si existe una etiqueta personalizada suscrita en el medio actual.

Puede monitorizar los metadatos temporizados escuchando los siguientes eventos, que notifican a la aplicación de la actividad relacionada:

* `MediaPlayerItemEvent.ITEM_CREATED`: La lista inicial de  `TimedMetadata` objetos está disponible después de  `MediaPlayerItem` crearla. Este evento notifica a la aplicación cuando esto sucede.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Para flujos en directo/lineales en los que el manifiesto/lista de reproducción se actualiza periódicamente, pueden aparecer etiquetas personalizadas adicionales en la lista de reproducción/manifiesto actualizado, por lo que se pueden agregar objetos TimedMetadata adicionales a la  `MediaPlayerItem.timedMetadata` propiedad. Este evento notifica a la aplicación cuando esto sucede.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Cada vez que se crea un nuevo  `TimedMetadata` objeto, el  `MediaPlayer` envía este evento. Este evento no se envía para el objeto `TimedMetadata` creado durante la fase de inicialización.

