---
title: Generar los metadatos DRM locales
description: Generar los metadatos DRM locales
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Generar los metadatos DRM locales{#generate-the-on-premises-drm-metadata}

A [!DNL CreateMetadata.jar] se incluye en la variable [!DNL create_metadata] carpeta. El objetivo de esta utilidad es crear metadatos DRM locales que inicien al cliente en la realización del proceso de individualización con el servidor de individualización local especificado.

1. Actualice la Implementación de referencia de DRM de Primetime: Herramientas de línea de comandos con los siguientes archivos:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

     Los dos archivos JAR pueden residir en el [!DNL Command Line Tools/libs] carpeta. El [!DNL createMetadata.properties] El archivo puede residir junto al [!DNL flashaccesstools.properties] archivo.

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Se incluye un [!DNL examplecreate.sh] secuencia de comandos que muestra una creación de metadatos de ejemplo. Asegúrese de configurar la URL del servidor de licencias y la URL del servidor de individualización en los archivos de script y de propiedades antes de intentar generar metadatos.

Las entradas para la utilidad son las siguientes:

* `createMetadata.properties` : archivo de propiedades que contiene una directiva predeterminada, ubicaciones de certificados, contraseñas, etc.
* `indivCert` - Archivo PKCS12 que contiene el certificado de transporte de individualización
* `indivURL` : URL del servidor de individualización local

El archivo de salida es un archivo de metadatos DRM local que consumirá el cliente DRM. Por ejemplo:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.
