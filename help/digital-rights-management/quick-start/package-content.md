---
title: Empaquetar contenido cifrado
description: Empaquetar contenido cifrado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Paquete de contenido cifrado{#package-encrypted-content}

1. Copie el directorio `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` en su sistema de archivos local.
1. En la carpeta local `Command Line Tools\`, actualice el archivo `flashaccesstools.properties` para que funcione con su servidor.

   Debe modificar al menos las siguientes propiedades:

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`: La ruta al certificado de servidor de licencias (normalmente termina con  [!DNL .cer],  [!DNL .der] o  [!DNL .pem]).

   * `encrypt.license.serverurl=[license-server-url]`: La URL del servidor de licencias, por ejemplo:     `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`: La ruta al certificado de transporte (normalmente termina con  [!DNL .cer],  [!DNL .der] o  [!DNL .pem]).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`: La ruta al certificado de Packager (termina con  [!DNL .pfx]).

   * `encrypt.sign.certpass=[password]`: La contraseña del certificado de Packager.
   >[!NOTE]
   >
   >Asegúrese de no codificar la contraseña.

1. Cree una directiva.

   En la carpeta local `Command Line Tools\`, ejecute el siguiente comando:

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   Este comando crea un archivo de directiva denominado [!DNL examplepolicy.pol] que utiliza la autenticación anónima del servidor de licencias (la opción `-x`).
1. Copie el archivo de vídeo MP4, FLV o F4V que desee cifrar en la carpeta local `Command Line Tools\` .
1. Empaquete el contenido.

   Digamos que el archivo de vídeo de origen es [!DNL sample.mp4]. En la carpeta local `Command Line Tools\`, ejecute el siguiente comando:

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >Si desea empaquetar contenido de HLS, HDS o DASH, debe utilizar una herramienta de empaquetado diferente, como [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. Copie los artefactos del archivo cifrado (en este caso [!DNL sample_encrypted.mp4] y [!DNL sample_encrypted.mp4.metadata]) en `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

En este punto ha completado la fase de empaquetado del proceso.

>[!NOTE]
>
>Para obtener información más detallada sobre las herramientas de línea de comandos para empaquetar contenido, crear políticas y mucho más, consulte [Herramientas de línea de comandos de Adobe Primetime DRM](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
