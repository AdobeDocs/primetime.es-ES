---
seo-title: Cifrado de contenido
title: Cifrado de contenido
uuid: 03f33473-bcd4-4e06-a823-e944897cb28e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Cifrando contenido{#encrypting-content}

El contenido de vídeo se cifra con el objeto `MediaEncrypter`. Puede cifrar archivos multimedia que solo incluyan pistas de audio. También puede aplicar solo codificación parcial; por ejemplo, para mejorar el rendimiento al cifrar contenido H.264 para dispositivos de gama inferior.

Para cifrar archivos multimedia mediante la API de Java:

1. Configure el entorno de desarrollo e incluya todos los archivos JAR mencionados en *Configuración del entorno de desarrollo* dentro del proyecto.
1. Cree una instancia `ServerCredential` para cargar las credenciales necesarias para la firma.
1. Cree una instancia `MediaEncrypter`. Utilice un `MediaEncryperFactory` si no sabe qué tipo de archivo tiene.

1. Especifique las opciones de codificación mediante un objeto `DRMParameters`.
1. Configure las opciones de firma utilizando un objeto `SignatureParameters` y pase la instancia `ServerCredential` a su método `setServerCredentials`.

1. Configure la información de la clave y la licencia mediante un objeto `V2KeyParameters`. Configure las directivas de DRM con el método `setPolicies`. Configure la información necesaria para que el cliente se ponga en contacto con el servidor de licencias llamando a los métodos `setLicenseServerUrl` y `setLicenseServerTransportCertificate`. Configure las opciones de cifrado CEK utilizando el método `setKeyProtectionOptions` y sus propiedades personalizadas mediante el método `setCustomProperties`. Finalmente, según el tipo de cifrado utilizado, convierta el objeto `DRMKeyParameters` al tipo adecuado ( `VideoDRMParameters`, `AudioDRMParameters`) y establezca las opciones de cifrado.

1. Cifre el contenido pasando los archivos de entrada y salida y las opciones de cifrado al método `MediaEncrypter.encryptContent`.

Para obtener el código de muestra que muestra cómo cifrar contenido, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` en el directorio Reference Implementation Command Line Tools [!DNL samples/] (Herramientas de línea de comandos de implementación de referencia).
