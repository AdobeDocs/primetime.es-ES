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

Invocar funciones de llamada de retorno para contenido, anuncios y capítulos.

```java
// Video Metadata Block 
vaMetadata.setVideoMetadataBlock(new VideoAnalyticsMetadata.VideoMetadataBlock() { 
    @Override 
    public HashMap<String, String> call() { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("myvideoid", "1234"); 
        result.put("mysdkversion", Version.getVersion()); 
  
        return result; 
    } 
}); 
  
// Ad Metadata Block invoked on every ad start 
vaMetadata.setAdMetadataBlock(new VideoAnalyticsMetadata.AdMetadataBlock() { 
    @Override 
    public HashMap<String, String> call(Ad ad) { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("myadid", "ad-1234"); 
        result.put("myad-sdkversion", Version.getVersion()); 
  
        return result; 
    } 
}); 
  
// Chapter Metadata Block invoked on every chapter start 
vaMetadata.setChapterMetadataBlock(new VideoAnalyticsMetadata.ChapterMetadataBlock() { 
    @Override 
    public HashMap<String, String> call(VideoAnalyticsChapterData chapter) { 
        HashMap<String, String> result = new HashMap<String, String>(); 
        result.put("mychapterid", "chapter-1234"); 
        result.put("mychapter-sdkversion", Version.getVersion()); 
  
        return result; 
    } 
});
```
