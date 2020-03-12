---
seo-title: Cifrado de contenido
title: Cifrado de contenido
uuid: 03f33473-bcd4-4e06-a823-e944897cb28e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Cifrado de contenido{#encrypting-content}

El contenido de vídeo se cifra con el `MediaEncrypter` objeto. Puede cifrar archivos multimedia que solo incluyan pistas de audio. También puede aplicar solo codificación parcial; por ejemplo, para mejorar el rendimiento al cifrar contenido H.264 para dispositivos de gama inferior.

Para cifrar archivos multimedia mediante la API de Java:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en *Configuración del entorno* de desarrollo dentro del proyecto.
1. Cree una `ServerCredential` instancia para cargar las credenciales necesarias para firmar.
1. Cree una `MediaEncrypter` instancia. Use un `MediaEncryperFactory` si no sabe qué tipo de archivo tiene.

1. Especifique las opciones de codificación mediante un `DRMParameters` objeto.
1. Defina las opciones de firma utilizando un `SignatureParameters` objeto y pase la `ServerCredential` instancia a su `setServerCredentials` método.

1. Configure la información de la clave y la licencia mediante un `V2KeyParameters` objeto. Configure las directivas de DRM con el `setPolicies` método . Configure la información necesaria para que el cliente se ponga en contacto con el servidor de licencias llamando a los `setLicenseServerUrl` métodos y `setLicenseServerTransportCertificate` . Configure las opciones de cifrado CEK mediante el `setKeyProtectionOptions` método y sus propiedades personalizadas mediante el `setCustomProperties` método . Por último, según el tipo de codificación utilizado, convierta el `DRMKeyParameters` objeto al tipo adecuado ( `VideoDRMParameters`, `AudioDRMParameters`) y defina las opciones de codificación.

1. Cifre el contenido pasando los archivos de entrada y salida y las opciones de codificación al `MediaEncrypter.encryptContent` método.

Para obtener el código de muestra que muestra cómo cifrar contenido, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` en el directorio Reference Implementation Command Line Tools (Herramientas de la línea de comandos de implementación de referencia) [!DNL samples/] .
