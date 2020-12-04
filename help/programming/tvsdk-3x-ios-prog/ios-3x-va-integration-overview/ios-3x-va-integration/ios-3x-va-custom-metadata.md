---
description: Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.
seo-description: Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.
seo-title: Implementar compatibilidad con metadatos personalizados
title: Implementar compatibilidad con metadatos personalizados
uuid: 229681f5-ff77-4321-8022-b8ccf2928fb3
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Implementar compatibilidad con metadatos personalizados {#implement-custom-metadata-support}

Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.

Las funciones de llamada de retorno se invocan justo antes de que se realice la llamada de seguimiento, de modo que la aplicación puede adjuntar los metadatos específicos de un anuncio o capítulo.

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
