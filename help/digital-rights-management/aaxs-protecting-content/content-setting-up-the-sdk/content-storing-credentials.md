---
title: Almacenamiento de credenciales
description: Almacenamiento de credenciales
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Almacenamiento de credenciales{#storing-credentials}

El SDK admite varias formas de almacenar credenciales (un certificado de clave pública y su clave privada asociada), incluso en un HSM o como archivo PKCS12. Las credenciales se utilizan cuando se requiere la clave privada (por ejemplo, para que el empaquetador firme los metadatos o para que el servidor de licencias descienda los datos cifrados con el servidor de licencias o la clave pública de transporte). Las claves privadas deben estar estrechamente vigiladas para garantizar la seguridad del contenido y del servidor de licencias. PKCS12 es un formato estándar para un archivo que contiene credenciales cifradas con una contraseña. La extensión de archivo .pfx se utiliza comúnmente para archivos de este formato.

>[!NOTE]
>
>Adobe recomienda utilizar un HSM para obtener la máxima seguridad. Para obtener más información, consulte las Directrices de implementación segura de acceso a Adobe .

>[!NOTE]
>
>Desde Java1.7, Sun Java de 64 bits para Windows no admite las interfaces PKCS11 que requiere el DRM de acceso de Adobe para comunicarse con dispositivos HSM. Si planea utilizar un HSM, utilice una versión de Java de 32 bits o un JDK que admita todas las interfaces PKCS11.

Puede mantener una clave privada en un módulo de seguridad de hardware (HSM) y utilizar el SDK para pasar las credenciales que obtenga del HSM. Para utilizar una credencial almacenada en un HSM, utilice un proveedor JCE que pueda comunicarse con un HSM para obtener un identificador de la clave privada. A continuación, pase el identificador de clave privada, el nombre del proveedor y el certificado que contiene la clave pública a `ServerCredentialFactory.getServerCredential()`.

El proveedor SunPKCS11 es un ejemplo de proveedor JCE que puede utilizarse para acceder a una clave privada en un HSM (consulte la documentación de Sun Java para obtener instrucciones sobre el uso de este proveedor). Algunos HSM también incluyen un SDK de Java que incluye un proveedor de JCE.

PEM y DER son dos formas de codificar un certificado de clave pública. PEM es una codificación base-64 y DER es una codificación binaria. Los archivos de certificado suelen utilizar la extensión .cer, .pem. o .der. Los certificados se utilizan en lugares donde solo se requiere la clave pública. Si un componente requiere únicamente la clave pública para funcionar, es mejor proporcionar a ese componente el certificado en lugar de un archivo de credenciales o PKCS12.
