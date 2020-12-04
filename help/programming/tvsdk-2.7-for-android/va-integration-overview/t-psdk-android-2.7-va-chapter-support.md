---
description: 'null'
seo-description: 'null'
seo-title: Implementar compatibilidad con capítulos
title: Implementar compatibilidad con capítulos
uuid: f62a8244-6393-4a38-9ae2-8ac31f6a8a06
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# Implementar compatibilidad con capítulos {#implement-chapter-support}

Puede definir y rastrear *capítulos personalizados* para el seguimiento de vídeo en aplicaciones basadas en TVSDK.

Los capítulos personalizados son administrados por la aplicación y se basan en datos CMS o de otra manera que la aplicación utiliza para definir capítulos.

>[!CAUTION]
>
>Los capítulos predeterminados no se admiten en el SDK 2.5 de Android.

1. Defina y rastree los capítulos personalizados.

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

