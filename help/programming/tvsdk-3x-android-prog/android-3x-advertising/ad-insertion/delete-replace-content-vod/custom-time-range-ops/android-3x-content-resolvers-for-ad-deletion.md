---
description: Puede utilizar varios solucionadores de contenido para gestionar diferentes operaciones de línea de tiempo.
seo-description: Puede utilizar varios solucionadores de contenido para gestionar diferentes operaciones de línea de tiempo.
seo-title: El contenido se resuelve para la eliminación o sustitución de publicidades
title: El contenido se resuelve para la eliminación o sustitución de publicidades
uuid: d43d54be-e04a-49dd-a695-e4e8f981ccb4
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '51'
ht-degree: 0%

---


# El contenido se resuelve para la eliminación o reemplazo de publicidades {#content-resolvers-for-ad-deletion-replacement}

Puede utilizar varios solucionadores de contenido para gestionar diferentes operaciones de línea de tiempo.

```java
public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
    List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
    MediaPlayerItemConfig itemConfig = item.getConfig(); 
    if(itemConfig) { 
        CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
        if (customRanges) { 
            List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
 
            if (timeRanges && timeRanges.size() > 0) { 
                //CustomRangeResolver is activated by the presence of CustomRanges 
                resolvers.add(new CustomRangeResolver()); 
            } 
        } 
        AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
        if (metadata) { 
            if (metadata instanceOf AuditudeSettings)  
            resolvers.add(new AuditudeResolver(getContext());                                      
        } 
    } 
    //Add your custom resolver if any 
    resolvers.add(MyOpportunityGenerator(item)); 
    return resolvers; 
} 
```
