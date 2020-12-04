---
description: Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.
seo-description: Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.
seo-title: Implementar compatibilidad con metadatos personalizados
title: Implementar compatibilidad con metadatos personalizados
uuid: 2186db58-10b0-43a6-840f-53ab289843ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Implementar compatibilidad con metadatos personalizados{#implement-custom-metadata-support}

Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.

Las funciones de llamada de retorno se invocan justo antes de que se realice la llamada de seguimiento, de modo que la aplicación puede adjuntar los metadatos específicos de un anuncio o capítulo.

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

