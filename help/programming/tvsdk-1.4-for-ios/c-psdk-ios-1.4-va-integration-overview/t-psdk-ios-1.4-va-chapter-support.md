---
title: Implementación de compatibilidad con capítulos
description: Implementación de compatibilidad con capítulos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Implementación de compatibilidad con capítulos{#implement-chapter-support}

Puede definir y rastrear capítulos para el seguimiento de vídeo en una aplicación basada en TVSDK de las siguientes maneras:

* Capítulos predeterminados, que TVSDK administra internamente.

  Un capítulo se define como el tiempo entre cada pausa publicitaria. Por ejemplo, el tiempo entre una pausa publicitaria del anuncio previo a la emisión y el primer anuncio durante la emisión se define como el primer capítulo.
* Los capítulos personalizados, que son administrados por la aplicación y se basan en datos de CMS o en otra forma que la aplicación utiliza para definir capítulos.

  Defina y rastree capítulos predeterminados o personalizados.

  ```
  // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
  
      vaTrackingMetadata.enableChapterTracking = YES; 
  
  // For custom chapter definitions, provide an array of chapters through the metadata:  
  // For example, 3 chapters of 60 second duration each: 
  
      NSMutableArray *chapters = [[[NSMutableArray alloc] init] autorelease]; 
  
      int chapterDuration = 60; 
      for (int i = 0; i < 3; i++) 
      { 
          PTVideoAnalyticsChapterData *chapterData =  
            [[[PTVideoAnalyticsChapterData alloc] init] autorelease]; 
          chapterData.name = [NSString stringWithFormat:@"chapter_%d", (i+1)]; 
          chapterData.range =  
            CMTimeRangeMake(CMTimeMakeWithSeconds(i * chapterDuration, 10000),  
            CMTimeMakeWithSeconds(chapterDuration, 10000)); 
  
          [chapters addObject:chapterData]; 
      } 
  
      vaTrackingMetadata.chapters = chapters; 
  
  // For default chapters, the application must not set custom chapters on the tracking metadata  
  // and simply enable chapters to be tracked by setting the boolean value as defined above.
  ```
