---
description: Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.
seo-description: Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.
seo-title: Implementar compatibilidad con metadatos personalizados
title: Implementar compatibilidad con metadatos personalizados
uuid: 068ef0b9-79a2-4e44-8a0a-01e9deb8e4a6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Implementar compatibilidad con metadatos personalizados {#implement-custom-metadata-support}

Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.

Las funciones de llamada de retorno se invocan justo antes de que se realice la llamada de seguimiento, de modo que la aplicación puede adjuntar los metadatos específicos de un anuncio o capítulo.

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

