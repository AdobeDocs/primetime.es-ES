---
description: TVSDK envía eventos de administración de derechos digitales (DRM) en respuesta a operaciones relacionadas con DRM, como cuando hay nuevos metadatos DRM disponibles. El reproductor puede implementar acciones en respuesta a estos eventos.
title: Eventos de DRM
exl-id: 712347f3-f103-4c08-ad19-af1dd59ac549
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Eventos de DRM{#drm-events}

TVSDK envía eventos de administración de derechos digitales (DRM) en respuesta a operaciones relacionadas con DRM, como cuando hay nuevos metadatos DRM disponibles. El reproductor puede implementar acciones en respuesta a estos eventos.

Para recibir notificaciones sobre todos los eventos relacionados con DRM, espere lo siguiente:

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
