---
description: TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM, como cuando nuevos metadatos DRM están disponibles.
title: Eventos DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Eventos DRM{#drm-events}

TVSDK distribuye eventos de administración de derechos digitales (DRM) como respuesta a operaciones relacionadas con DRM, como cuando nuevos metadatos DRM están disponibles.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, registre una implementación de `MediaPlayer.DRMEventListener` que incluya la siguiente llamada de retorno.

| Evento | Significado |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | Hay nuevos metadatos DRM disponibles. |

