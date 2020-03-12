---
seo-title: Examen del contenido de archivos cifrados
title: Examen del contenido de archivos cifrados
uuid: 2132fac7-5f11-4308-b511-ed4f216527a6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Examen del contenido de archivos cifrados {#examining-encrypted-file-content}

Para examinar el contenido de un archivo FLV o F4V mediante la API de Java, lleve a cabo los siguientes pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en [Configuración del entorno](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) de desarrollo dentro del proyecto.
1. Cree una `MediaEncrypter` instancia.
1. Pase el archivo cifrado al `MediaEncrypter.examineEncryptedContent` método, que devuelve un `KeyMetaData` objeto.
1. Inspeccione la información dentro del `KeyMetaData` objeto.

Para obtener un código de muestra que muestre cómo extraer metadatos DRM de un archivo cifrado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` en el directorio &quot;samples&quot; de la línea de comandos de implementación de referencia Herramientas de comandos.
