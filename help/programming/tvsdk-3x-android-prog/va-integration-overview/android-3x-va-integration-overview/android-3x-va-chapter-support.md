---
title: Implementación de compatibilidad con capítulos
description: Implementación de compatibilidad con capítulos
copied-description: true
exl-id: 2db335b3-1d9b-4339-b1b6-e12ee0f06566
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Implementación de compatibilidad con capítulos {#implement-chapter-support}

Puede definir y rastrear *personalizado* capítulos para el seguimiento de vídeo en aplicaciones basadas en TVSDK.

La aplicación gestiona los capítulos personalizados y se basan en datos de CMS o en otra forma que la aplicación utiliza para definir capítulos.

>[!CAUTION]
>
>Los capítulos predeterminados no son compatibles con Android TVSDK 3.0.

Defina y rastree capítulos personalizados.

```java
// First, enable chapter tracking by setting   
// enableChapterTracking to true: 
 
vaMetadata.enableChapterTracking(true); 
// For custom chapter definitions, provide  
// an array list of chapters through the metadata. 
// For example: 3 chapters of 60 second duration each 
 
List<VideoAnalyticsChapterData> chapters =  
  new ArrayList<VideoAnalyticsChapterData>(); 
 
Int chapterDuration = 60; 
for (var i = 0; i < 3; i++) { 
    VideoAnalyticsChapterData chapterData =  
      new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
    chapterData.setName("chapter_" + (i+1)); 
    chapters.add(chapterData); 
} 
 
vaMetadata.setChapters(chapters); 
```
