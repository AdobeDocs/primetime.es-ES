---
title: Cifrado de contenido
description: Cifrado de contenido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Cifrado de contenido{#encrypting-content}

El contenido de vídeo se cifra con `MediaEncrypter` objeto. Puede cifrar archivos multimedia que sólo incluyan pistas de audio. También puede aplicar sólo el cifrado parcial; por ejemplo, para mejorar el rendimiento al cifrar contenido H.264 para dispositivos de gama baja.

Para cifrar archivos multimedia mediante la API de Java:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en *Configuración del entorno de desarrollo* dentro del proyecto.
1. Crear un `ServerCredential` para cargar las credenciales necesarias para la firma.
1. Crear un `MediaEncrypter` ejemplo. Utilice un `MediaEncryperFactory` si no sabe qué tipo de archivo tiene.

1. Especifique las opciones de cifrado mediante una `DRMParameters` objeto.
1. Configurar las opciones de firma mediante una `SignatureParameters` y pase el `ServerCredential` a su instancia `setServerCredentials` método.

1. Configurar la clave y la información de licencia mediante una `V2KeyParameters` objeto. Definir las políticas de DRM mediante la variable `setPolicies` método. Configure la información que necesita el cliente para ponerse en contacto con el servidor de licencias llamando al `setLicenseServerUrl` y `setLicenseServerTransportCertificate` métodos. Configure las opciones de cifrado CEK utilizando `setKeyProtectionOptions` y sus propiedades personalizadas utilizando el método `setCustomProperties` método. Finalmente, según el tipo de cifrado utilizado, convierta el `DRMKeyParameters` al tipo adecuado ( `VideoDRMParameters`, `AudioDRMParameters`) y establezca las opciones de cifrado.

1. Cifre el contenido pasando los archivos de entrada y salida y las opciones de cifrado al `MediaEncrypter.encryptContent` método.

Para ver el código de ejemplo que muestra cómo cifrar contenido, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` en las herramientas de línea de comandos de implementación de referencia [!DNL samples/] directorio.
