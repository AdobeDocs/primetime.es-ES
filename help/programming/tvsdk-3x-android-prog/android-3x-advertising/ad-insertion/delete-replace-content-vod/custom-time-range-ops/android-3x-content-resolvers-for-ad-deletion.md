---
description: Puede utilizar varias resoluciones de contenido para gestionar distintas operaciones de cronología.
title: Resoluciones de contenido para la eliminación/sustitución de anuncios
exl-id: e215ae64-894a-41db-a407-6be0e7464a82
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '34'
ht-degree: 0%

---

# Resoluciones de contenido para la eliminación/sustitución de anuncios {#content-resolvers-for-ad-deletion-replacement}

Puede utilizar varias resoluciones de contenido para gestionar distintas operaciones de cronología.

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
