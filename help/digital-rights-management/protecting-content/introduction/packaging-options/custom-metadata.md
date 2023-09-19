---
title: Metadatos personalizados
description: Metadatos personalizados
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Metadatos personalizados {#custom-metadata}

Utilice esto para añadir pares de clave/valor personalizados a los metadatos de contenido que la aplicación del servidor puede interpretar.

El formato de metadatos para el contenido DRM de Primetime permite incluir pares clave/valor personalizados en el momento del empaquetado. El servidor de licencias puede procesar estos metadatos personalizados durante la emisión de la licencia. Los metadatos son independientes de una directiva DRM de Primetime y pueden ser únicos para cada sección de contenido.

Ejemplo de caso de uso: durante una fase beta, puede incluir la propiedad personalizada `Release:BETA` en el momento del embalaje. Los servidores de licencias pueden enviar licencias a este contenido durante el período beta. Sin embargo, una vez que caduca el periodo Beta, los servidores de licencias no permiten el acceso al contenido.
