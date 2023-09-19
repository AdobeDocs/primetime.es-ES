---
description: Puede proporcionar metadatos personalizados sobre el contenido, los anuncios y las llamadas de seguimiento de capítulos mediante funciones de devolución de llamada.
title: Implementación de compatibilidad con metadatos personalizados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# Implementación de compatibilidad con metadatos personalizados{#implement-custom-metadata-support}

Puede proporcionar metadatos personalizados sobre el contenido, los anuncios y las llamadas de seguimiento de capítulos mediante funciones de devolución de llamada.

Las funciones de llamada de retorno se invocan justo antes de que se realice la llamada de seguimiento, por lo que la aplicación puede adjuntar los metadatos específicos de un anuncio o capítulo.

1. Invocar funciones de llamada de retorno para contenido, anuncios y capítulos.

   ```
   // Video Metadata Block 
   vaMetadata.videoMetadataBlock = function():Object { 
       return {"myvideoid":"1234", "mysdkversion":Version.version} 
   }; 
   
   // Ad Metadata Block invoked on every ad start 
   vaMetadata.adMetadataBlock = function(ad:Ad):Object { 
       return {"myadid":"ad-1234", "myad-sdkversion":Version.version} 
   }; 
   
   // Chapter Metadata Block invoked on every chapter start 
   vaMetadata.chapterMetadataBlock = function(chapter:VideoAnalyticsChapterData) { 
       return {"mychapterid":"chapter-1234", "mychapter-sdkversion":Version.version} 
   };
   ```
