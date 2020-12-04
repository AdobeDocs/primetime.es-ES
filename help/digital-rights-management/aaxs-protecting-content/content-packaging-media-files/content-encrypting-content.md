---
seo-title: Cifrado de contenido
title: Cifrado de contenido
uuid: ea71154e-557b-447e-bc14-208232f00be1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Cifrando contenido{#encrypting-content}

La codificación de contenido FLV y F4V implica el uso de un objeto `MediaEncrypter`. También puede empaquetar archivos FLV y F4V que solo contengan pistas de audio. Al cifrar el contenido H.264 para dispositivos de gama baja, puede resultar práctico aplicar solo cifrado parcial para mejorar el rendimiento. En estos casos, un archivo F4V puede cifrarse parcialmente mediante el método `F4VDRMParameters.setVideoEncryptionLevel`.

Para cifrar un archivo FLV o F4V mediante la API de Java, lleve a cabo los siguientes pasos:

1. Configure el entorno de desarrollo e incluya todos los archivos JAR mencionados en Configuración del entorno de desarrollo dentro del proyecto.
1. Cree una instancia `ServerCredential` para cargar las credenciales necesarias para la firma.
1. Cree una instancia `MediaEncrypter`. Utilice un `MediaEncryperFactory` si no sabe qué tipo de archivo tiene. De lo contrario, puede crear un `FLVEncrypter` o `F4VEncrypter` directamente.
1. Especifique las opciones de codificación mediante un objeto `DRMParameters`.
1. Configure las opciones de firma utilizando un objeto `SignatureParameters` y pase la instancia `ServerCredential` a su método `setServerCredentials`.
1. Configure la información de la clave y la licencia mediante un objeto `V2KeyParameters`. Configure las directivas mediante el método `setPolicies`. Configure la información necesaria para que el cliente se ponga en contacto con el servidor de licencias llamando a los métodos `setLicenseServerUrl` y `setLicenseServerTransportCertificate`. Configure las opciones de cifrado CEK utilizando el método `setKeyProtectionOptions` y sus propiedades personalizadas mediante el método `setCustomProperties`. Por último, según el tipo de cifrado utilizado, convierta el objeto `DRMKeyParameters` en uno de `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters` o `F4VDRMParameters` y establezca las opciones de cifrado.
1. Cifre el contenido pasando los archivos de entrada y salida y las opciones de cifrado al método `MediaEncrypter.encryptContent`.

Para obtener un código de muestra que muestre cómo cifrar contenido, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` en el directorio &quot;samples&quot; de la línea de comandos de implementación de referencia.
