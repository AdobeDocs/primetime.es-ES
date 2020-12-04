---
seo-title: Metadatos personalizados
title: Metadatos personalizados
uuid: 99bdef62-32a9-4fd0-919c-5a2594e8d17e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# Metadatos personalizados {#custom-metadata}

Utilice esta opción para agregar pares de clave/valor personalizados a los metadatos de contenido que la aplicación de servidor pueda interpretar.

El formato de metadatos del contenido de DRM de Primetime le permite incluir pares de clave/valor personalizados en el momento del empaquetado. El servidor de licencias puede procesar estos metadatos personalizados durante la emisión de la licencia. Los metadatos están separados de una directiva DRM de Primetime y pueden ser únicos para cada sección de contenido.

Ejemplo de caso de uso: Durante una fase beta, puede incluir la propiedad personalizada `Release:BETA` en el momento del empaquetado. Los servidores de licencias pueden entregar licencias a este contenido durante el período beta. Sin embargo, una vez caducado el período Beta, los servidores de licencias no permiten el acceso al contenido.
