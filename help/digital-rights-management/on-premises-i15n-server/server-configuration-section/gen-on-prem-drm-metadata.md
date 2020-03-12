---
seo-title: Generar los metadatos DRM locales
title: Generar los metadatos DRM locales
uuid: 89d53924-1a8d-42d4-a716-ce4f4566b6bf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Generar los metadatos DRM locales{#generate-the-on-premises-drm-metadata}

Se incluye una [!DNL CreateMetadata.jar] utilidad en la [!DNL create_metadata] carpeta. El objetivo de esta utilidad es crear un archivo de metadatos DRM en las instalaciones que iniciará al cliente para realizar el proceso de individualización con el servidor de individualización en las instalaciones especificado.

1. Actualice la implementación de referencia de DRM de Primetime - Herramientas de línea de comandos con los siguientes archivos:

   * [!DNL CreateMetadata.jar]
   * [!DNL commons-cli-1.2.jar]
   * [!DNL createMetadata.properties]

      Los dos archivos JAR pueden residir en la [!DNL Command Line Tools/libs] carpeta. El [!DNL createMetadata.properties] archivo puede residir junto al [!DNL flashaccesstools.properties] archivo.

<!--<a id="example_2116349CA33642CD9293EAD94A532ED8"></a>-->

Se incluye una [!DNL examplecreate.sh] secuencia de comandos que muestra una creación de metadatos de muestra. Asegúrese de configurar la URL del servidor de licencias y la URL del servidor de individualización tanto en los archivos de secuencias de comandos como en los archivos de propiedades antes de intentar generar metadatos.

Las entradas para la utilidad son las siguientes:

* `createMetadata.properties` - Archivo de propiedades que contiene una directiva predeterminada, ubicaciones de certificados y contraseñas, etc.
* `indivCert` - Archivo PKCS12 que contiene el certificado de transporte de individualización
* `indivURL` - Dirección URL del servidor de individualización local

El archivo de salida es un archivo de metadatos DRM On Premises que el cliente DRM consumirá. Por ejemplo:

```
java -jar libs/CreateMetadata.jar -c createMetadata.properties -indivCert i15n_transport.cer
-indivURL https://[YOURINDIVSERVER:PORT] onpremdrm.metadata
```

.