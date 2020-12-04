---
description: TVSDK distribuye eventos de metadatos temporizados y genera metadatos temporizados cada vez que se encuentran etiquetas predeterminadas o personalizadas o cuando una lista de reproducción cambia en un manifiesto. Los eventos se envían en el orden en que aparecen en el manifiesto.
seo-description: TVSDK distribuye eventos de metadatos temporizados y genera metadatos temporizados cada vez que se encuentran etiquetas predeterminadas o personalizadas o cuando una lista de reproducción cambia en un manifiesto. Los eventos se envían en el orden en que aparecen en el manifiesto.
seo-title: Eventos de metadatos temporizados
title: Eventos de metadatos temporizados
uuid: 69c43701-6ffa-45fe-a104-fe81391222e7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Eventos de metadatos temporizados{#timed-metadata-events}

TVSDK distribuye eventos de metadatos temporizados y genera metadatos temporizados cada vez que se encuentran etiquetas predeterminadas o personalizadas o cuando una lista de reproducción cambia en un manifiesto. Los eventos se envían en el orden en que aparecen en el manifiesto.

El reproductor implementa acciones en función de los siguientes eventos:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`:: Se distribuye cuando se procesan metadatos temporizados de ID3.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`:: Se distribuye cuando se procesan metadatos temporizados y no se detecta ninguna oportunidad.

