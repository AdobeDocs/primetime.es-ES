---
title: Examen del contenido de archivos cifrados
description: Examen del contenido de archivos cifrados
copied-description: true
exl-id: a8a61d1c-c259-4346-9a71-6741f70697ae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Examen del contenido de archivos cifrados {#examining-encrypted-file-content}

Para examinar el contenido de un archivo FLV o F4V mediante la API de Java, realice los siguientes pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en [Configuración del entorno de desarrollo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) dentro del proyecto.
1. Crear un `MediaEncrypter` ejemplo.
1. Pase el archivo cifrado a `MediaEncrypter.examineEncryptedContent` método, que devuelve un valor `KeyMetaData` objeto.
1. Inspect la información dentro de `KeyMetaData` objeto.

Para ver un código de ejemplo que muestra cómo extraer metadatos DRM de un archivo cifrado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` en el directorio &quot;samples&quot; de Herramientas de línea de comandos de implementación de referencia.
