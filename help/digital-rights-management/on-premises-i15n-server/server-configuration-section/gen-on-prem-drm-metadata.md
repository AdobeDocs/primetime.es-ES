---
title: Generar los metadatos DRM locales
description: Generar los metadatos DRM locales
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---


# Generar los metadatos DRM On-Premise{#generate-the-on-premises-drm-metadata}

Se incluye una utilidad [!DNL CreateMetadata.jar] en la carpeta [!DNL create_metadata]. El objetivo de esta utilidad es crear un DRM de On-Premies que inicie al cliente para realizar el proceso de individualización con el servidor de individualización On-Premies especificado.

1. Actualice la Implementación de referencia de DRM de Primetime - Herramientas de línea de comandos con los siguientes archivos:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      Los dos archivos JAR pueden residir en la carpeta [!DNL Command Line Tools/libs]. El archivo [!DNL createMetadata.properties] puede residir junto al archivo [!DNL flashaccesstools.properties].

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Se incluye una secuencia de comandos [!DNL examplecreate.sh] que muestra una creación de metadatos de ejemplo. Asegúrese de configurar la URL del servidor de licencias y la URL del servidor de individualización tanto en los archivos de script como de propiedades antes de intentar generar metadatos.

Las entradas para la utilidad son las siguientes:

* `createMetadata.properties` - Archivo de propiedades que contiene una directiva predeterminada, ubicaciones de certificados y contraseñas, etc.
* `indivCert` - Archivo PKCS12 que contiene el certificado de transporte de individualización
* `indivURL` - URL del servidor de individualización On Premies

El archivo de salida es un archivo de metadatos DRM On-Premies que el cliente DRM consumirá. Por ejemplo:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.