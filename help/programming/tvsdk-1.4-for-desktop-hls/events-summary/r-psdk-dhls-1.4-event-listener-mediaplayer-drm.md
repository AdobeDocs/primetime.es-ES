---
description: TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM como, por ejemplo, cuando hay disponibles nuevos metadatos DRM.
seo-description: TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM como, por ejemplo, cuando hay disponibles nuevos metadatos DRM.
seo-title: Eventos DRM
title: Eventos DRM
uuid: f1da5b31-3fad-4bb4-8aa3-3925d5f0e123
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Eventos DRM{#drm-events}

TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM como, por ejemplo, cuando hay disponibles nuevos metadatos DRM.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, busque eventos `DRMMetadataInfoEvent` de DRM con el `MediaPlayer` objeto.

| Evento | Significado |
|---|---|
| DRMMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | Hay disponibles nuevos metadatos DRM. |