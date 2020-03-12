---
seo-title: Cifrado de contenido
title: Cifrado de contenido
uuid: ea71154e-557b-447e-bc14-208232f00be1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Cifrado de contenido{#encrypting-content}

La codificación de contenido FLV y F4V implica el uso de un `MediaEncrypter` objeto. También puede empaquetar archivos FLV y F4V que solo contengan pistas de audio. Al cifrar el contenido H.264 para dispositivos de gama baja, puede resultar práctico aplicar solo cifrado parcial para mejorar el rendimiento. En estos casos, un archivo F4V puede cifrarse parcialmente mediante el `F4VDRMParameters.setVideoEncryptionLevel`método .

Para cifrar un archivo FLV o F4V mediante la API de Java, lleve a cabo los siguientes pasos:

1. Configure su entorno de desarrollo e incluya todos los archivos JAR mencionados en Configuración del entorno de desarrollo dentro del proyecto.
1. Cree una `ServerCredential` instancia para cargar las credenciales necesarias para firmar.
1. Cree una `MediaEncrypter` instancia. Use un `MediaEncryperFactory` si no sabe qué tipo de archivo tiene. De lo contrario, puede crear un `FLVEncrypter` o `F4VEncrypter` directamente.
1. Especifique las opciones de codificación mediante un `DRMParameters` objeto.
1. Defina las opciones de firma utilizando un `SignatureParameters` objeto y pase la `ServerCredential` instancia a su `setServerCredentials` método.
1. Configure la información de la clave y la licencia mediante un `V2KeyParameters` objeto. Configure las directivas mediante el `setPolicies` método . Configure la información necesaria para que el cliente se ponga en contacto con el servidor de licencias llamando a los `setLicenseServerUrl` métodos y `setLicenseServerTransportCertificate` . Configure las opciones de cifrado CEK mediante el `setKeyProtectionOptions` método y sus propiedades personalizadas mediante el `setCustomProperties` método . Por último, según el tipo de codificación utilizado, convierta el `DRMKeyParameters` objeto en uno de `VideoDRMParameters`, `AudioDRMParameters`, `FLVDRMParameters`o `F4VDRMParameters`, y defina las opciones de codificación.
1. Cifre el contenido pasando los archivos de entrada y salida y las opciones de codificación al `MediaEncrypter.encryptContent` método.

Para obtener un código de muestra que muestre cómo cifrar contenido, consulte `com.adobe.flashaccess.samples.mediapackager.EncryptContent` en el directorio Reference Implementation Command Line Tools &quot;samples&quot; (Ejemplos).
