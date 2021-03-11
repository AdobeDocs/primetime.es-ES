---
description: TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM, como cuando nuevos metadatos DRM están disponibles.
title: Eventos DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# Eventos DRM{#drm-events}

TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM, como cuando nuevos metadatos DRM están disponibles.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, escuche `DRMMetadataInfoEvent` para los eventos DRM con el objeto `MediaPlayer`.

| Evento | Significado |
|---|---|
| DRMMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | Hay nuevos metadatos DRM disponibles. |