---
description: 'null'
seo-description: 'null'
seo-title: Implementar compatibilidad con capítulos
title: Implementar compatibilidad con capítulos
uuid: 85d14b83-7910-4f5d-9ef2-511de916abd6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Implementar compatibilidad con capítulos {#implement-chapter-support}

Puede definir y rastrear capítulos para el seguimiento de vídeo en una aplicación basada en TVSDK de las siguientes formas:

* Los capítulos predeterminados, que TVSDK administra internamente.

   Un capítulo se define como el tiempo entre cada pausa publicitaria. Por ejemplo, el tiempo entre una pausa publicitaria previa y la primera mitad del resumen se define como el primer capítulo.
* Los capítulos personalizados, que son administrados por la aplicación y se basan en datos CMS o de otra manera que la aplicación utiliza para definir capítulos.

   Defina y rastree los capítulos predeterminados o personalizados.

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

