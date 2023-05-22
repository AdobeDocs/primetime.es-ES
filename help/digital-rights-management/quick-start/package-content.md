---
title: Empaquetar contenido cifrado
description: Empaquetar contenido cifrado
copied-description: true
exl-id: e5792917-8172-48b0-8792-7a7e942596c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Empaquetar contenido cifrado{#package-encrypted-content}

1. Copie el `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` a su sistema de archivos local.
1. En su local `Command Line Tools\` , actualice la carpeta `flashaccesstools.properties` para trabajar con el servidor.

   Debe modificar al menos las siguientes propiedades:

   * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`: La ruta al certificado del servidor de licencias (normalmente termina con [!DNL .cer], [!DNL .der] o [!DNL .pem]).

   * `encrypt.license.serverurl=[license-server-url]`: URL del servidor de licencias, p. ej.:    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`.

   * `encrypt.license.servercert=[transport-certificate.cer]`: La ruta al certificado de transporte (normalmente termina con [!DNL .cer], [!DNL .der], o [!DNL .pem]).

   * `encrypt.sign.certfile=[packager-credentials.pfx]`: La ruta al certificado del empaquetador (termina con [!DNL .pfx]).

   * `encrypt.sign.certpass=[password]`: La contraseña del certificado de Packager.
   >[!NOTE]
   >
   >Asegúrese de no codificar la contraseña.

1. Cree una directiva.

   En su local `Command Line Tools\` , ejecute el siguiente comando:

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   Este comando crea un archivo de directivas denominado [!DNL examplepolicy.pol] que utiliza la autenticación anónima del servidor de licencias (el `-x` opción).
1. Copie el archivo de vídeo MP4, FLV o F4V que desee cifrar en el archivo local `Command Line Tools\` carpeta.
1. Empaquete el contenido.

   Digamos que su archivo de vídeo de origen es [!DNL sample.mp4]. En su local `Command Line Tools\` , ejecute el siguiente comando:

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >Si desea empaquetar contenido de HLS, HDS o DASH, debe utilizar una herramienta de empaquetado diferente, como [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. Copie los artefactos de archivo cifrados (en este caso, ) [!DNL sample_encrypted.mp4] y [!DNL sample_encrypted.mp4.metadata]) a `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

En este punto ha completado la fase de empaquetado del proceso.

>[!NOTE]
>
>Para obtener información más detallada sobre las herramientas de la línea de comandos para empaquetar contenido, crear directivas y mucho más, consulte [Herramientas de línea de comandos DRM de Adobe Primetime](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
