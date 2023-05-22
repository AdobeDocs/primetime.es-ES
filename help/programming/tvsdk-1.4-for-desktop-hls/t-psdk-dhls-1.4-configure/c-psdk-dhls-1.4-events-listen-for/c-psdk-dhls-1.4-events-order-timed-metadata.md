---
description: TVSDK envía eventos de metadatos cronometrados y genera metadatos cronometrados cada vez que se encuentran etiquetas predeterminadas o personalizadas, o cuando cambia una lista de reproducción en un manifiesto. Los eventos se distribuyen en el orden en que aparecen en el manifiesto.
title: Eventos de metadatos cronometrados
exl-id: 4c58b06e-5f70-452c-a743-55c4b6206711
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Eventos de metadatos cronometrados{#timed-metadata-events}

TVSDK envía eventos de metadatos cronometrados y genera metadatos cronometrados cada vez que se encuentran etiquetas predeterminadas o personalizadas, o cuando cambia una lista de reproducción en un manifiesto. Los eventos se distribuyen en el orden en que aparecen en el manifiesto.

El reproductor implementa acciones basadas en los siguientes eventos:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: Se envía cuando se procesa un ID3 de metadatos cronometrados.
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: Se envía cuando se procesan los metadatos cronometrados y no se detecta ninguna oportunidad.
