---
title: Codificación de contenido
description: Codificación de contenido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Codificación de contenido{#encrypting-content}

El contenido de vídeo se cifra con el objeto `MediaEncrypter`. Puede cifrar archivos multimedia que solo incluyan pistas de audio. También puede aplicar solo cifrado parcial; por ejemplo, para mejorar el rendimiento al cifrar contenido H.264 para dispositivos de gama inferior.

Para cifrar archivos multimedia mediante la API de Java:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en *Configuración del entorno de desarrollo* dentro del proyecto.
1. Cree una instancia `ServerCredential` para cargar las credenciales necesarias para firmar.
1. Cree una instancia `MediaEncrypter`. Utilice un `MediaEncryperFactory` si no sabe qué tipo de archivo tiene.

1. Especifique las opciones de codificación utilizando un objeto `DRMParameters`.
1. Establezca las opciones de firma utilizando un objeto `SignatureParameters` y pase la instancia `ServerCredential` a su método `setServerCredentials`.

1. Establezca la información de clave y licencia mediante un objeto `V2KeyParameters`. Establezca las directivas de DRM utilizando el método `setPolicies`. Configure la información necesaria para que el cliente se ponga en contacto con el servidor de licencias llamando a los métodos `setLicenseServerUrl` y `setLicenseServerTransportCertificate`. Establezca las opciones de cifrado CEK utilizando el método `setKeyProtectionOptions` y sus propiedades personalizadas utilizando el método `setCustomProperties`. Finalmente, según el tipo de cifrado utilizado, convierta el objeto `DRMKeyParameters` al tipo adecuado ( `VideoDRMParameters`, `AudioDRMParameters`) y establezca las opciones de cifrado.

1. Codifique el contenido pasando los archivos de entrada y salida y las opciones de cifrado al método `MediaEncrypter.encryptContent` .

Para obtener código de muestra que muestre cómo cifrar contenido, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` en el directorio Herramientas de línea de comandos de implementación de referencia [!DNL samples/] .
