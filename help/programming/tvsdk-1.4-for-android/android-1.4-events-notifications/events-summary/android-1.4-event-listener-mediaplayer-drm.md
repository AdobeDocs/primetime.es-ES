---
description: TVSDK envía eventos de administración de derechos digitales (DRM) en respuesta a operaciones relacionadas con DRM, como cuando hay nuevos metadatos DRM disponibles.
title: Eventos de DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Eventos de DRM{#drm-events}

TVSDK envía eventos de administración de derechos digitales (DRM) en respuesta a operaciones relacionadas con DRM, como cuando hay nuevos metadatos DRM disponibles.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, registre una implementación de `MediaPlayer.DRMEventListener` que incluye la siguiente llamada de retorno.

| Evento | Significado |
|---|---|
| [onDRMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | Hay nuevos metadatos DRM disponibles. |
