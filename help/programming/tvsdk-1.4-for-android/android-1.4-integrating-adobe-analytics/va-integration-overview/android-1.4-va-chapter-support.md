---
description: 'null'
seo-description: 'null'
seo-title: Implementar compatibilidad con capítulos
title: Implementar compatibilidad con capítulos
uuid: 5b39e494-85ad-43bb-ab56-a55797aa4ef7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Implementar compatibilidad con capítulos {#implement-chapter-support}

Puede definir y rastrear capítulos para el seguimiento de vídeo en una aplicación basada en TVSDK de las siguientes formas:

* Los capítulos predeterminados, que TVSDK administra internamente.

   Un capítulo se define como el tiempo entre cada pausa publicitaria. Por ejemplo, el tiempo entre una pausa publicitaria previa y la primera mitad del resumen se define como el primer capítulo.
* Los capítulos personalizados, que son administrados por la aplicación y se basan en datos CMS o de otra manera que la aplicación utiliza para definir capítulos.

1. Defina y rastree los capítulos predeterminados o personalizados.

   ```java
   // First, enable chapter tracking by setting  
   // the Boolean 'enableChapterTracking' to true: 
   
   vaMetadata.enableChapterTracking(true); 
   // For custom chapter definitions, provide an array list of chapters  
   // through the metadata. 
   // For example: 3 chapters of 60 second duration each 
   
   List<VideoAnalyticsChapterData> chapters = new ArrayList<VideoAnalyticsChapterData>(); 
   
   Int chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       VideoAnalyticsChapterData chapterData =  
         new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
       chapterData.setName("chapter_" + (i+1)); 
       chapters.add(chapterData); 
   } 
   
   vaMetadata.setChapters(chapters); 
   // For default chapters, the application must not set  
   // custom chapters on the tracking metadata 
   // and simply enable chapters to be tracked by setting  
   // the boolean value as defined above.
   ```
