---
description: TVSDK envía eventos de administración de derechos digitales (DRM) en respuesta a operaciones relacionadas con DRM, como cuando hay nuevos metadatos DRM disponibles.
title: Eventos de DRM
exl-id: 65a02744-8973-418d-9a9c-53a2a313f631
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Eventos de DRM{#drm-events}

TVSDK envía eventos de administración de derechos digitales (DRM) en respuesta a operaciones relacionadas con DRM, como cuando hay nuevos metadatos DRM disponibles.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, espere `DRMMetadataInfoEvent` para eventos DRM con `MediaPlayer` objeto.

| Evento | Significado |
|---|---|
| DTMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | Hay nuevos metadatos DRM disponibles. |
