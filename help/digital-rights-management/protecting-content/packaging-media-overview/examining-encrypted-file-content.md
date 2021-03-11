---
title: Examen del contenido de un archivo cifrado
description: Examen del contenido de un archivo cifrado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Examen del contenido del archivo cifrado{#examining-encrypted-file-content}

Puede examinar el contenido de un archivo multimedia cifrado mediante la API de Java.

Para examinar el contenido del archivo cifrado:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR. Consulte *Configuración del SDK* para su proyecto.
1. Cree una instancia `MediaEncrypter`.
1. Pase el archivo cifrado al método `MediaEncrypter.examineEncryptedContent` , que devuelve un objeto `KeyMetaData`.

1. Inspect la información del objeto `KeyMetaData`.

Para obtener código de ejemplo que describe cómo extraer metadatos DRM de un archivo cifrado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` en el directorio Herramientas de línea de comandos de implementación de referencia [!DNL samples/] .
