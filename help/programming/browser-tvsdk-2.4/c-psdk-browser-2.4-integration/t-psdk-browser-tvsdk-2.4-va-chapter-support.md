---
title: Implementación de compatibilidad con capítulos
description: Implementación de compatibilidad con capítulos
copied-description: true
exl-id: 8a962706-50cd-41c2-96a7-6af1b24145a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# Implementación de compatibilidad con capítulos{#implement-chapter-support}

Un capítulo se define como el tiempo entre cada pausa publicitaria. Por ejemplo, el tiempo entre una pausa publicitaria del anuncio previo a la emisión y el primer anuncio durante la emisión se define como el primer capítulo. Puede definir y rastrear capítulos de para el seguimiento de vídeo en una aplicación basada en TVSDK de Browser mediante capítulos personalizados. La aplicación administra los capítulos personalizados y se basan en datos de CMS o en otra forma que la aplicación utiliza para definir capítulos.

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
