---
description: 'null'
seo-description: 'null'
seo-title: Implementar compatibilidad con capítulos
title: Implementar compatibilidad con capítulos
uuid: 70f10621-febe-4443-84e7-ce95bec53377
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Implementar compatibilidad con capítulos{#implement-chapter-support}

Un capítulo se define como el tiempo entre cada pausa publicitaria. Por ejemplo, el tiempo entre una pausa publicitaria previa y la primera mitad del resumen se define como el primer capítulo. Puede definir y rastrear capítulos para el seguimiento de vídeo en una aplicación basada en TVSDK del explorador mediante capítulos personalizados. La aplicación administra los capítulos personalizados en función de los datos de CMS o de otro modo que la aplicación utiliza para definir capítulos.

1. Defina y rastree los capítulos personalizados.

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

