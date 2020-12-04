---
seo-title: Examen del contenido de archivos cifrados
title: Examen del contenido de archivos cifrados
uuid: 2132fac7-5f11-4308-b511-ed4f216527a6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Examen del contenido de archivos cifrados {#examining-encrypted-file-content}

Para examinar el contenido de un archivo FLV o F4V mediante la API de Java, lleve a cabo los siguientes pasos:

1. Configure el entorno de desarrollo e incluya todos los archivos JAR mencionados en [Configuración del entorno de desarrollo](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) dentro del proyecto.
1. Cree una instancia `MediaEncrypter`.
1. Pase el archivo cifrado al método `MediaEncrypter.examineEncryptedContent`, que devuelve un objeto `KeyMetaData`.
1. Inspect la información dentro del objeto `KeyMetaData`.

Para obtener un código de muestra que muestre cómo extraer metadatos DRM de un archivo cifrado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` en el directorio Reference Implementation Command Line Tools &quot;samples&quot; (Ejemplos).
