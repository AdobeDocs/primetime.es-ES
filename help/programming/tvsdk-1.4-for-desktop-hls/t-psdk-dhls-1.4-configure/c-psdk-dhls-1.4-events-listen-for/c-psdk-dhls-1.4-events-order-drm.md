---
description: TVSDK distribuye eventos de administración de derechos digitales (DRM) en respuesta a operaciones relacionadas con DRM como, por ejemplo, cuando hay disponibles nuevos metadatos DRM. El reproductor puede implementar acciones en respuesta a estos eventos.
seo-description: TVSDK distribuye eventos de administración de derechos digitales (DRM) en respuesta a operaciones relacionadas con DRM como, por ejemplo, cuando hay disponibles nuevos metadatos DRM. El reproductor puede implementar acciones en respuesta a estos eventos.
seo-title: Eventos DRM
title: Eventos DRM
uuid: 729fe524-1047-4188-b4e6-96bfc5af4ae0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Eventos DRM{#drm-events}

TVSDK distribuye eventos de administración de derechos digitales (DRM) en respuesta a operaciones relacionadas con DRM como, por ejemplo, cuando hay disponibles nuevos metadatos DRM. El reproductor puede implementar acciones en respuesta a estos eventos.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, escuche lo siguiente:

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

El siguiente ejemplo muestra una progresión típica:

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```

