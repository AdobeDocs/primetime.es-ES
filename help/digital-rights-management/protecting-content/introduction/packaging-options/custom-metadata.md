---
title: Metadatos personalizados
description: Metadatos personalizados
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# Metadatos personalizados {#custom-metadata}

Utilice esto para agregar pares de clave/valor personalizados a los metadatos de contenido que la aplicación de servidor pueda interpretar.

El formato de metadatos para el contenido de Primetime DRM permite incluir pares personalizados de clave/valor en el momento del empaquetado. El servidor de licencias puede procesar estos metadatos personalizados durante la emisión de la licencia. Los metadatos están separados de una directiva de DRM de Primetime y pueden ser únicos para cada sección de contenido.

Ejemplo de caso de uso: Durante una fase beta, puede incluir la propiedad personalizada `Release:BETA` en el momento del empaquetado. Los servidores de licencias pueden entregar licencias a este contenido durante el periodo Beta. Sin embargo, una vez transcurrido el período beta, los servidores de licencias no permiten el acceso al contenido.
