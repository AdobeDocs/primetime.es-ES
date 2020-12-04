---
seo-title: Empaquetar contenido cifrado
title: Empaquetar contenido cifrado
uuid: 1e271167-107d-41df-8a7c-3075cb3acc0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Empaquetar contenido cifrado{#package-encrypted-content}

1. Copie el directorio `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` en su sistema de archivos local.
1. En la carpeta `Command Line Tools\` local, actualice el archivo `flashaccesstools.properties` para que funcione con el servidor.

   Debe modificar al menos las siguientes propiedades:

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`:: La ruta de acceso al certificado de servidor de licencias (generalmente termina con  [!DNL .cer]o  [!DNL .der] con  [!DNL .pem]).

   * `encrypt.license.serverurl=[license-server-url]`:: Dirección URL del servidor de licencias, por ejemplo:     `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`:: Ruta de acceso al certificado de transporte (generalmente termina con  [!DNL .cer],  [!DNL .der] o  [!DNL .pem]).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`:: Ruta de acceso al certificado de Packager (esto termina con  [!DNL .pfx]).

   * `encrypt.sign.certpass=[password]`:: La contraseña del certificado de Packager.
   >[!NOTE]
   >
   >Asegúrese de no codificar la contraseña.

1. Cree una directiva.

   En la carpeta local `Command Line Tools\`, ejecute el siguiente comando:

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   Este comando crea un archivo de política denominado [!DNL examplepolicy.pol] que utiliza la autenticación anónima del servidor de licencias (la opción `-x`).
1. Copie el archivo de vídeo MP4, FLV o F4V que desea cifrar en la carpeta local `Command Line Tools\`.
1. Empaquete el contenido.

   Supongamos que el archivo de vídeo de origen es [!DNL sample.mp4]. En la carpeta local `Command Line Tools\`, ejecute el siguiente comando:

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >Si desea empaquetar contenido de HLS, HDS o DASH, debe utilizar una herramienta de empaquetador diferente, como [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. Copie los artefactos del archivo cifrado (en este caso [!DNL sample_encrypted.mp4] y [!DNL sample_encrypted.mp4.metadata]) en `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

En este punto, ha completado la fase de empaquetado del proceso.

>[!NOTE]
>
>Para obtener información más detallada sobre las herramientas de la línea de comandos para empaquetar contenido, crear políticas y mucho más, consulte [Herramientas de la línea de comandos de Adobe Primetime DRM](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
