---
title: Implementar compatibilidad con capítulos
description: Implementar compatibilidad con capítulos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---


# Implementar compatibilidad con capítulos{#implement-chapter-support}

Un capítulo se define como el tiempo entre cada pausa publicitaria. Por ejemplo, el tiempo entre una pausa publicitaria pre-roll y la primera mitad de la emisión se define como el primer capítulo. Puede definir y rastrear capítulos para el seguimiento de vídeo en una aplicación basada en TVSDK de explorador mediante capítulos personalizados. La aplicación administra los capítulos personalizados basados en datos de CMS o en otra forma que la aplicación utilice para definir capítulos.

1. Defina y rastree capítulos personalizados.

   ```js
   vaObj.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata: 
   // For example: 3 chapters of 60 second duration each 
   var chapters = []; 
   var chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       var chapterData = new AdobePSDK.VA.VideoAnalyticsChapterData("chapter_" + (i+1), i * chapterDuration, chapterDuration, (i+1)); 
       chapters.push(chapterData); 
   } 
   
   vaObj.chapters = chapters;
   ```

