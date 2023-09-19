---
title: Cifrado de contenido
description: Cifrado de contenido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Cifrado de contenido{#encrypting-content}

El cifrado de contenido FLV y F4V implica el uso de un `MediaEncrypter` objeto. También puede empaquetar archivos FLV y F4V que sólo contengan pistas de audio. Al cifrar contenido H.264 para dispositivos de gama baja, puede resultar práctico aplicar únicamente cifrado parcial para mejorar el rendimiento. En estos casos, un archivo F4V puede cifrarse parcialmente utilizando `F4VDRMParameters.setVideoEncryptionLevel`método.

Para cifrar un archivo FLV o F4V mediante la API de Java, realice los siguientes pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en Configuración del entorno de desarrollo dentro del proyecto.
1. Crear un `ServerCredential` para cargar las credenciales necesarias para la firma.
1. Crear un `MediaEncrypter` ejemplo. Utilice un `MediaEncryperFactory` si no sabe qué tipo de archivo tiene. De lo contrario, puede crear un `FLVEncrypter` o `F4VEncrypter` directamente.
1. Especifique las opciones de cifrado mediante una `DRMParameters` objeto.
1. Configurar las opciones de firma mediante una `SignatureParameters` y pase el `ServerCredential` a su instancia `setServerCredentials` método.
1. Configurar la clave y la información de licencia mediante una `V2KeyParameters` objeto. Configurar las directivas mediante `setPolicies` método. Configure la información que necesita el cliente para ponerse en contacto con el servidor de licencias llamando al `setLicenseServerUrl` y `setLicenseServerTransportCertificate` métodos. Configure las opciones de cifrado CEK utilizando `setKeyProtectionOptions` y sus propiedades personalizadas utilizando el método `setCustomProperties` método. Finalmente, según el tipo de cifrado utilizado, convierta el `DRMKeyParameters` objeto a uno de `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters`, o `F4VDRMParameters`y configure las opciones de cifrado.
1. Cifre el contenido pasando los archivos de entrada y salida y las opciones de cifrado al `MediaEncrypter.encryptContent` método.

Para ver el código de ejemplo que muestra cómo cifrar contenido, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` en el directorio &quot;samples&quot; de Herramientas de línea de comandos de implementación de referencia.
