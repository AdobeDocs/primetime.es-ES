---
description: TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM como, por ejemplo, cuando hay disponibles nuevos metadatos DRM.
seo-description: TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM como, por ejemplo, cuando hay disponibles nuevos metadatos DRM.
seo-title: Eventos DRM
title: Eventos DRM
uuid: c4d96e06-2268-4e38-9d05-68ccbe912484
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Eventos DRM{#drm-events}

TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM como, por ejemplo, cuando hay disponibles nuevos metadatos DRM.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, registre una implementación de `MediaPlayer.DRMEventListener` que incluya la siguiente llamada de retorno.

| Evento | Significado |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo))`(DRMMetadataInfo drmMetadataInfo)` | Hay disponibles nuevos metadatos DRM. |

