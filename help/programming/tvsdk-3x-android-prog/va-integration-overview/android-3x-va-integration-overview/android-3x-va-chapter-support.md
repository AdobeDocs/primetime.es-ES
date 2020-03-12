---
description: 'null'
seo-description: 'null'
seo-title: Implementar compatibilidad con capítulos
title: Implementar compatibilidad con capítulos
uuid: 6e2c3994-d28b-489f-ae60-9b876125a871
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Implementar compatibilidad con capítulos {#implement-chapter-support}

Puede definir y rastrear capítulos *personalizados* para el seguimiento de vídeo en aplicaciones basadas en TVSDK.

Los capítulos personalizados son administrados por la aplicación y se basan en datos CMS o de otra manera que la aplicación utiliza para definir capítulos.

>[!CAUTION]
>
>Los capítulos predeterminados no son compatibles con el TVSDK de Android 3.0.

Defina y rastree los capítulos personalizados.

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
