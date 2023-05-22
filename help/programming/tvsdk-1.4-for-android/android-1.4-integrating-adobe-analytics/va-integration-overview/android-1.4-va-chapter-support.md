---
title: Implementación de compatibilidad con capítulos
description: Implementación de compatibilidad con capítulos
copied-description: true
exl-id: f86af555-4eba-4bc8-a323-41f65f23f4cc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Implementación de compatibilidad con capítulos {#implement-chapter-support}

Puede definir y rastrear capítulos para el seguimiento de vídeo en una aplicación basada en TVSDK de las siguientes maneras:

* Capítulos predeterminados, que TVSDK administra internamente.

   Un capítulo se define como el tiempo entre cada pausa publicitaria. Por ejemplo, el tiempo entre una pausa publicitaria del anuncio previo a la emisión y el primer anuncio durante la emisión se define como el primer capítulo.
* Los capítulos personalizados, que son administrados por la aplicación y se basan en datos de CMS o en otra forma que la aplicación utiliza para definir capítulos.

1. Defina y rastree capítulos predeterminados o personalizados.

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
