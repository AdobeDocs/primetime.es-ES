---
title: Implementación de compatibilidad con capítulos
description: Implementación de compatibilidad con capítulos
copied-description: true
exl-id: c6d9300e-33ce-4948-af5b-f28945fd47e4
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

   Defina y rastree capítulos predeterminados o personalizados.

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
   
       vaMetadata.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example: 3 chapters of 60 second duration each 
   
       var chapters:Vector.<VideoAnalyticsChapterData> = new Vector.<VideoAnalyticsChapterData>(); 
       var chapterDuration:int = 60; 
       for (var i:int = 0; i < 3; i++) { 
           var chapterData:VideoAnalyticsChapterData =  
             new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration); 
           chapterData.name = "chapter_%d" + (i+1); 
   
           chapters.push(chapterData); 
       } 
   
       vaMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above. 
   ```
