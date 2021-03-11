---
title: Codificación de contenido
description: Codificación de contenido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Codificación de contenido{#encrypting-content}

La codificación de contenido FLV y F4V implica el uso de un objeto `MediaEncrypter`. También puede empaquetar archivos FLV y F4V que contengan solo pistas de audio. Al cifrar contenido H.264 para dispositivos de gama baja, puede ser práctico aplicar solo cifrado parcial para mejorar el rendimiento. En estos casos, un archivo F4V puede cifrarse parcialmente mediante el método `F4VDRMParameters.setVideoEncryptionLevel`.

Para cifrar un archivo FLV o F4V utilizando la API de Java, siga estos pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en Configuración del entorno de desarrollo dentro del proyecto.
1. Cree una instancia `ServerCredential` para cargar las credenciales necesarias para firmar.
1. Cree una instancia `MediaEncrypter`. Utilice un `MediaEncryperFactory` si no sabe qué tipo de archivo tiene. De lo contrario, puede crear un `FLVEncrypter` o `F4VEncrypter` directamente.
1. Especifique las opciones de codificación utilizando un objeto `DRMParameters`.
1. Establezca las opciones de firma utilizando un objeto `SignatureParameters` y pase la instancia `ServerCredential` a su método `setServerCredentials`.
1. Establezca la información de clave y licencia mediante un objeto `V2KeyParameters`. Establezca las políticas utilizando el método `setPolicies`. Configure la información necesaria para que el cliente se ponga en contacto con el servidor de licencias llamando a los métodos `setLicenseServerUrl` y `setLicenseServerTransportCertificate`. Establezca las opciones de cifrado CEK utilizando el método `setKeyProtectionOptions` y sus propiedades personalizadas utilizando el método `setCustomProperties`. Por último, según el tipo de cifrado utilizado, convierta el objeto `DRMKeyParameters` en uno de `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters` o `F4VDRMParameters` y configure las opciones de cifrado.
1. Codifique el contenido pasando los archivos de entrada y salida y las opciones de cifrado al método `MediaEncrypter.encryptContent` .

Para obtener un código de ejemplo que muestre cómo cifrar contenido, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` en el directorio &quot;muestras&quot; de las herramientas de la línea de comandos de implementación de referencia.
