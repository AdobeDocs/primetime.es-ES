---
description: La propiedad MediaPlayerItem.timedMetadata proporciona acceso a todos los objetos TimedMetadata creados a partir de etiquetas de lista de reproducción/manifiesto o de etiquetas ID3 dentro del flujo de medios. La propiedad MediaPlayerItem.hasTimedMetadata indica si hay una etiqueta personalizada suscrita en el contenido actual.
title: Notificaciones para etiquetas de manifiesto
exl-id: 1a91fa47-edd5-4496-9755-17c906a3cf54
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Notificaciones para etiquetas de manifiesto{#notifications-for-manifest-tags}

La propiedad MediaPlayerItem.timedMetadata proporciona acceso a todos los objetos TimedMetadata creados a partir de etiquetas de lista de reproducción/manifiesto o de etiquetas ID3 dentro del flujo de medios. La propiedad MediaPlayerItem.hasTimedMetadata indica si hay una etiqueta personalizada suscrita en el contenido actual.

Puede monitorizar los metadatos cronometrados si escucha los siguientes eventos, que notifican a la aplicación la actividad relacionada:

* `MediaPlayerItemEvent.ITEM_CREATED`: la lista inicial de `TimedMetadata` está disponible después de que `MediaPlayerItem` se ha creado. Este evento notifica a la aplicación cuando esto sucede.

* `MediaPlayerItemEvent.ITEM_UPDATED`: para flujos activos/lineales en los que el manifiesto/lista de reproducción se actualiza periódicamente, podrían aparecer etiquetas personalizadas adicionales en la lista de reproducción/manifiesto actualizado, por lo que se podrían agregar objetos TimedMetadata adicionales a la `MediaPlayerItem.timedMetadata` propiedad. Este evento notifica a la aplicación cuando esto sucede.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Cada vez que se crea un nuevo `TimedMetadata` se crea, este evento lo distribuye el `MediaPlayer`. Este evento no se envía para `TimedMetadata` objeto creado durante la fase de inicialización.
