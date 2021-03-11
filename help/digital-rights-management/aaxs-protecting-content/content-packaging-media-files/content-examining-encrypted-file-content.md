---
title: Examen del contenido de un archivo cifrado
description: Examen del contenido de un archivo cifrado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Examen del contenido del archivo cifrado {#examining-encrypted-file-content}

Para examinar el contenido de un archivo FLV o F4V mediante la API de Java, siga estos pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en [Configuración del entorno de desarrollo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) dentro del proyecto.
1. Cree una instancia `MediaEncrypter`.
1. Pase el archivo cifrado al método `MediaEncrypter.examineEncryptedContent` , que devuelve un objeto `KeyMetaData`.
1. Inspect la información del objeto `KeyMetaData`.

Para obtener un código de ejemplo que muestre cómo extraer metadatos DRM de un archivo cifrado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` en el directorio &quot;muestras&quot; de las herramientas de la línea de comandos de implementación de referencia.
