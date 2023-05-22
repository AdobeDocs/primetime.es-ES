---
title: Examen del contenido de archivos cifrados
description: Examen del contenido de archivos cifrados
copied-description: true
exl-id: df1fd04d-016e-4770-bcb9-97bfe2d39260
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Examen del contenido de archivos cifrados{#examining-encrypted-file-content}

Puede examinar el contenido de un archivo multimedia cifrado mediante la API de Java.

Para examinar el contenido de un archivo cifrado:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR. Consulte *Configuración del SDK* para su proyecto.
1. Crear un `MediaEncrypter` ejemplo.
1. Pase el archivo cifrado a `MediaEncrypter.examineEncryptedContent` método, que devuelve un valor `KeyMetaData` objeto.

1. Inspect la información dentro de `KeyMetaData` objeto.

Para ver un código de ejemplo que describe cómo extraer metadatos DRM de un archivo cifrado, consulte `com.adobe.flashaccess.samples.mediapackager.ExamineContent` en las herramientas de línea de comandos de implementación de referencia [!DNL samples/] directorio.
