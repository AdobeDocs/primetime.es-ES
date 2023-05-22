---
description: TVSDK envía eventos de administración de derechos digitales (DRM) en respuesta a operaciones relacionadas con DRM, como cuando hay nuevos metadatos DRM disponibles.
title: Eventos de DRM
exl-id: 8a3bd8c7-1e76-4d26-8f88-e29eb0a0e1b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
