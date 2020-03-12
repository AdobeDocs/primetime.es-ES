---
description: Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.
seo-description: Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.
seo-title: Implementar compatibilidad con metadatos personalizados
title: Implementar compatibilidad con metadatos personalizados
uuid: 6e23311c-a393-4485-919e-4cf6412789b1
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Implementar compatibilidad con metadatos personalizados{#implement-custom-metadata-support}

Puede proporcionar metadatos personalizados sobre el contenido, las publicidades y las llamadas de seguimiento de capítulos mediante las funciones de llamada de retorno.

Las funciones de llamada de retorno se invocan justo antes de que se realice la llamada de seguimiento, de modo que la aplicación puede adjuntar los metadatos específicos de un anuncio o capítulo.

1. Invocar funciones de llamada de retorno para contenido, anuncios y capítulos.

   ```js
   vaObj.videoMetadataBlock = function() { 
       return { 
           "name" : "my-video", 
           "genre" : "comedy" 
       }; 
   } 
   
   vaObj.adMetadataBlock = function(ad) { 
       return { 
           "name" : "my-ad", 
           "category" : "automotive" 
       }; 
   } 
   
   vaObj.chapterMetadataBlock = function(chapter) { 
       return { 
           "name" : "my-chapter", 
           "type" : "quartile" 
       }; 
   }
   ```

