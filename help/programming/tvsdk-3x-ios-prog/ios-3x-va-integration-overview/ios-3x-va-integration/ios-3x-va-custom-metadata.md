---
description: Puede proporcionar metadatos personalizados sobre el contenido, los anuncios y las llamadas de seguimiento de capítulos mediante funciones de devolución de llamada.
title: Implementación de compatibilidad con metadatos personalizados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# Implementación de compatibilidad con metadatos personalizados {#implement-custom-metadata-support}

Puede proporcionar metadatos personalizados sobre el contenido, los anuncios y las llamadas de seguimiento de capítulos mediante funciones de devolución de llamada.

Las funciones de llamada de retorno se invocan justo antes de que se realice la llamada de seguimiento, por lo que la aplicación puede adjuntar los metadatos específicos de un anuncio o capítulo.

1. Invocar funciones de llamada de retorno para contenido, anuncios y capítulos.

   ```
   // Video Metadata Block 
       vaTrackingMetadata.videoMetadataBlock = ^NSDictionary *() 
       { 
           return @{ 
                    @"myvideoid": @"1234", 
                    @"mysdkversion": [PTSDK apiVersion] 
                    }; 
       }; 
   
   // Ad Metadata Block invoked on every ad start 
       vaTrackingMetadata.adMetadataBlock = ^NSDictionary *(PTAd *ad) 
       { 
           return @{ 
                    @"myadid": @"ad-1234", 
                    @"myad-sdkversion": [PTSDK apiVersion] 
                    }; 
       }; 
   
   // Chapter Metadata Block invoked on every chapter start 
       vaTrackingMetadata.chapterMetadataBlock = ^NSDictionary *(PTVideoAnalyticsChapterData *chapter) 
       { 
           return @{ 
                    @"mychapterid": @"chapter-1234", 
                    @"mychapter-sdkversion": [PTSDK apiVersion] 
                    }; 
       };
   ```
