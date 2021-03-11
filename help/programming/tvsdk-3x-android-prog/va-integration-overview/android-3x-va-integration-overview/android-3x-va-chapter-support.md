---
title: Implementar compatibilidad con capítulos
description: Implementar compatibilidad con capítulos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---


# Implementar compatibilidad con capítulos {#implement-chapter-support}

Puede definir y rastrear capítulos *personalizados* para el seguimiento de vídeo en aplicaciones basadas en TVSDK.

Los capítulos personalizados los gestiona la aplicación y se basan en datos de CMS o en otra forma que la aplicación utilice para definir capítulos.

>[!CAUTION]
>
>Los capítulos predeterminados no son compatibles con el TVSDK para Android 3.0.

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
