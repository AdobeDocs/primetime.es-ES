---
description: Puede utilizar varios solucionadores de contenido para gestionar diferentes operaciones de línea de tiempo.
seo-description: Puede utilizar varios solucionadores de contenido para gestionar diferentes operaciones de línea de tiempo.
seo-title: El contenido se resuelve para la eliminación o sustitución de publicidades
title: El contenido se resuelve para la eliminación o sustitución de publicidades
uuid: 2954ce0f-aed2-4a85-8e53-d4e89d1497b6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '51'
ht-degree: 0%

---


# El contenido se resuelve para la eliminación o reemplazo de publicidades {#content-resolvers-for-ad-deletion-replacement}

Puede utilizar varios solucionadores de contenido para gestionar diferentes operaciones de línea de tiempo.

```java
List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
MetadataNode metadata = (MetadataNode) resource.getMetadata(); 
if (metadata != null) { 
    if (metadata.containsKey(DefaultMetadataKeys.TIME_RANGES_METADATA_KEY.getValue())) { 
        String timeRangeType = metadata.getValue(DefaultMetadataKeys.TIME_RANGES_METADATA_KEY.getValue()); 
        if (timeRangeType.equals(TimeRangeCollection.TIME_RANGE_TYPE_DELETE)) { 
            contentResolvers.add(new DeleteContentResolver()); 
        } else if (timeRangeType.equals(TimeRangeCollection.TIME_RANGE_TYPE_REPLACE)) { 
            contentResolvers.add(new DeleteContentResolver()); 
        } else if (timeRangeType.equals(TimeRangeCollection.TIME_RANGE_TYPE_MARK)) { 
            contentResolvers.add(new CustomAdMarkersContentResolver()); 
        } 
    } 
    if (metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue())) { 
        contentResolvers.add(new AuditudeResolver(context)); 
    } else if (metadata.containsKey(DefaultMetadataKeys.JSON_METADATA_KEY.getValue())) { 
        contentResolvers.add(new MetadataResolver()); 
    } 
} 
return contentResolvers;
```

