---
seo-title: Almacenamiento de credenciales
title: Almacenamiento de credenciales
uuid: a9e9db72-c921-4c28-ad1d-3fd3c2283f14
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Almacenamiento de credenciales{#storing-credentials}

El SDK de DRM de Primetime admite diferentes formas de almacenar credenciales, incluido el uso de un módulo de seguridad de hardware (HSM) o como archivo PKCS12. El SDK utiliza una credencial (certificado de clave pública y clave privada asociada) cuando se requiere la clave privada. Por ejemplo, el empaquetador utiliza una credencial para firmar metadatos; el servidor de licencias utiliza una credencial para descifrar datos cifrados con el servidor de licencias o la clave pública de transporte.

Debe proteger de cerca las claves privadas para garantizar la seguridad del contenido y del servidor de licencias. PKCS12 es un formato de archivo estándar para almacenar credenciales cifradas con una contraseña. (También puede cifrar y firmar el propio archivo PKCS12). La extensión de archivo [!DNL .pfx] se utiliza comúnmente para los archivos que admiten este formato.

>[!NOTE]
>
>Adobe recomienda utilizar un HSM para una máxima seguridad.
>
>Consulte la guía *DRM Secure Deployment Guidelines* de Adobe Primetime.

>[!NOTE]
>
>A partir de Java 1.7, Sun Java de 64 bits para Windows ya no admite las interfaces PKCS11 que Primetime DRM requiere para la comunicación con dispositivos HSM. Si planea utilizar un HSM, debe utilizar una versión de 32 bits de Java o un JDK que admita las interfaces PKCS11 completas.

Puede mantener una clave privada en un HSM y utilizar el SDK de DRM de Primetime para pasar las credenciales que obtiene del HSM. Si desea utilizar una credencial almacenada en un HSM, debe utilizar un proveedor JCE que pueda comunicarse con un HSM para obtener un identificador de la clave privada. Luego debe pasar el identificador de clave privada, el nombre del proveedor y el certificado que incluye la clave pública a `ServerCredentialFactory.getServerCredential()`.

El proveedor SunPKCS11 representa un ejemplo de proveedor JCE que puede utilizar para acceder a una clave privada en un HSM. Algunos HSM también se incluyen con un SDK de Java que se incluye con un proveedor JCE.

Consulte la documentación de Sun Java para obtener instrucciones sobre cómo utilizar este proveedor.

PEM y DER son formas de codificar un certificado de clave pública. PEM es una codificación base-64 y DER es una codificación binaria. Los archivos de certificado suelen utilizar la extensión [!DNL .cer], [!DNL .pem] o [!DNL .der]. Los certificados se utilizan cuando solo se requiere una clave pública. Si un componente requiere únicamente la clave pública para funcionar, se recomienda proporcionar ese componente con el certificado en lugar de un archivo de credenciales o PKCS12.
