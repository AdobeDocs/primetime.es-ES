---
title: Almacenamiento de credenciales
description: Almacenamiento de credenciales
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Almacenamiento de credenciales{#storing-credentials}

El SDK admite varias formas de almacenar credenciales (un certificado de clave pública y su clave privada asociada), incluso en un HSM o como archivo PKCS12. Las credenciales se utilizan cuando se requiere la clave privada (por ejemplo, para que el empaquetador firme los metadatos o para que el servidor de licencias descifre los datos cifrados con el servidor de licencias o la clave pública de transporte). Las claves privadas deben protegerse cuidadosamente para garantizar la seguridad del contenido y del servidor de licencias. PKCS12 es un formato estándar para un archivo que contiene una credencial cifrada con una contraseña. La extensión de archivo .pfx se utiliza comúnmente para archivos de este formato.

>[!NOTE]
>
>El Adobe recomienda utilizar un HSM para una máxima seguridad. Para obtener más información, consulte las Directrices de implementación segura de Acceso a Adobe.

>[!NOTE]
>
>A partir de Java1.7, Sun Java de 64 bits para Windows no admite las interfaces PKCS11 que requiere DRM de acceso de Adobe para poder comunicarse con dispositivos HSM. Si planea utilizar un HSM, utilice una versión de 32 bits de Java o un JDK que admita las interfaces PKCS11 completas.

Puede mantener una clave privada en un Módulo de seguridad de hardware (HSM) y utilizar el SDK para pasar las credenciales que obtiene del HSM. Para utilizar una credencial almacenada en un HSM, utilice un proveedor JCE que pueda comunicarse con un HSM para obtener un identificador para la clave privada. A continuación, pase el identificador de clave privada, el nombre del proveedor y el certificado que contiene la clave pública a `ServerCredentialFactory.getServerCredential()`.

El proveedor SunPKCS11 es un ejemplo de proveedor JCE que se puede utilizar para acceder a una clave privada en un HSM (consulte la documentación de Sun Java para obtener instrucciones sobre el uso de este proveedor). Algunos HSM también incluyen un SDK de Java que incluye un proveedor JCE.

PEM y DER son dos formas de codificar un certificado de clave pública. PEM es una codificación en base 64 y DER es una codificación binaria. Los archivos de certificado suelen utilizar la extensión .cer, .pem. o .der. Los certificados se utilizan en lugares donde solo se requiere la clave pública. Si un componente solo requiere la clave pública para funcionar, es mejor proporcionar ese componente con el certificado en lugar de una credencial o archivo PKCS12.
