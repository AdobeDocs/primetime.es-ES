---
description: La propiedad MediaPlayerItem.timedMetadata proporciona acceso a todos los objetos TimedMetadata creados a partir de etiquetas de lista de reproducción/manifiesto o de etiquetas ID3 en el flujo de medios.
title: Notificaciones para etiquetas de manifiesto
exl-id: a8a3cada-d796-460a-bd8f-fc4a2703e7f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Notificaciones para etiquetas de manifiesto{#notifications-for-manifest-tags}

La propiedad MediaPlayerItem.timedMetadata proporciona acceso a todos los objetos TimedMetadata creados a partir de etiquetas de lista de reproducción/manifiesto o de etiquetas ID3 en el flujo de medios.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

El `MediaPlayerItem.hasTimedMetadata` indica si existe una etiqueta personalizada suscrita en el contenido actual. Puede monitorizar los metadatos cronometrados si escucha el `Events.TimedMetadataEvent`, que la instancia de MediaPlayer envía cada vez que se crea un nuevo `TimedMetadata` se ha creado el objeto.
