---
description: TVSDK envía eventos de metadatos temporizados y genera metadatos temporizados cada vez que se encuentran etiquetas predeterminadas o personalizadas o cuando una lista de reproducción cambia en un manifiesto. Los eventos se envían en el orden en que aparecen en el manifiesto.
title: Eventos de metadatos temporizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Eventos de metadatos temporizados{#timed-metadata-events}

TVSDK envía eventos de metadatos temporizados y genera metadatos temporizados cada vez que se encuentran etiquetas predeterminadas o personalizadas o cuando una lista de reproducción cambia en un manifiesto. Los eventos se envían en el orden en que aparecen en el manifiesto.

El reproductor implementa acciones en función de los siguientes eventos:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: Se envía cuando se procesan metadatos temporizados de ID3.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: Se envía cuando se procesan metadatos temporizados y no se ha detectado ninguna oportunidad.

