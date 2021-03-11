---
title: Almacenamiento de credenciales
description: Almacenamiento de credenciales
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Almacenamiento de credenciales{#storing-credentials}

El SDK de DRM de Primetime admite diferentes formas de almacenar credenciales, incluido el uso de un módulo de seguridad de hardware (HSM) o como archivo PKCS12. El SDK utiliza una credencial (certificado de clave pública y clave privada asociada) cuando se requiere la clave privada. Por ejemplo, el empaquetador utiliza una credencial para firmar metadatos; el servidor de licencias utiliza una credencial para descifrar datos cifrados con el servidor de licencias o la clave pública de transporte.

Debe proteger estrictamente las claves privadas para garantizar la seguridad de su contenido y del servidor de licencias. PKCS12 es un formato de archivo estándar para almacenar las credenciales cifradas con una contraseña. (También puede cifrar y firmar el propio archivo PKCS12). La extensión de archivo [!DNL .pfx] se utiliza comúnmente para archivos que admiten este formato.

>[!NOTE]
>
>Adobe recomienda utilizar un HSM para obtener la máxima seguridad.
>
>Consulte la guía *Adobe Primetime DRM Secure Deployment Guidelines* .

>[!NOTE]
>
>Desde Java 1.7, Sun Java de 64 bits para Windows ya no es compatible con las interfaces PKCS11 que exige Primetime DRM para la comunicación con dispositivos HSM. Si planea utilizar un HSM, debe utilizar una versión de Java de 32 bits o utilizar un JDK que admita las interfaces PKCS11 completas.

Puede mantener una clave privada en un HSM y utilizar el SDK de DRM de Primetime para pasar las credenciales que obtenga del HSM. Si desea utilizar una credencial almacenada en un HSM, debe utilizar un proveedor JCE que pueda comunicarse con un HSM para obtener un identificador de la clave privada. A continuación, debe pasar el identificador de clave privada, el nombre del proveedor y el certificado que incluye la clave pública a `ServerCredentialFactory.getServerCredential()`.

El proveedor SunPKCS11 representa un ejemplo de proveedor JCE que puede utilizar para acceder a una clave privada en un HSM. Algunos HSM también se incluyen con un SDK de Java que está empaquetado con un proveedor de JCE.

Consulte la documentación de Sun Java para obtener instrucciones sobre cómo utilizar este proveedor.

PEM y DER son formas de codificar un certificado de clave pública. PEM es una codificación base-64 y DER es una codificación binaria. Los archivos de certificado suelen utilizar la extensión [!DNL .cer], [!DNL .pem] o [!DNL .der]. Los certificados se utilizan donde solo se requiere una clave pública. Si un componente requiere únicamente la clave pública para funcionar, se recomienda proporcionar ese componente con el certificado en lugar de con una credencial o un archivo PKCS12.
