---
seo-title: Examen del contenido de archivos cifrados
title: Examen del contenido de archivos cifrados
uuid: 1b3318f6-0850-43f2-9127-c72ea81a1bdf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Examen del contenido de archivos cifrados{#examining-encrypted-file-content}

Puede examinar el contenido de un archivo multimedia cifrado mediante la API de Java.

Para examinar el contenido del archivo cifrado:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR. Consulte *Configuración del SDK* para su proyecto.
1. Cree una `MediaEncrypter` instancia.
1. Pase el archivo cifrado al `MediaEncrypter.examineEncryptedContent` método, que devuelve un `KeyMetaData` objeto.

1. Inspeccione la información dentro del `KeyMetaData` objeto.

Para obtener un código de muestra que describe cómo extraer metadatos DRM de un archivo cifrado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` en el directorio Herramientas de línea de comandos de implementación de referencia [!DNL samples/] .
