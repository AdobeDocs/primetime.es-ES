---
title: Almacenamiento de credenciales
description: Almacenamiento de credenciales
copied-description: true
exl-id: ceb1bc19-56a0-47ce-affd-ce4ecb896c3b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Almacenamiento de credenciales{#storing-credentials}

El SDK de DRM de Primetime admite diferentes formas de almacenar credenciales, incluido el uso de un Módulo de seguridad de hardware (HSM) o como un archivo PKCS12. El SDK utiliza una credencial (certificado de clave pública y clave privada asociada) cuando se requiere la clave privada. Por ejemplo, el empaquetador utiliza una credencial para firmar metadatos; el servidor de licencias utiliza una credencial para descifrar datos que se han cifrado con el servidor de licencias o la clave pública de transporte.

Debe proteger estrechamente las claves privadas para garantizar la seguridad del contenido y del servidor de licencias. PKCS12 es un formato de archivo estándar para almacenar credenciales cifradas con una contraseña. (También puede cifrar y firmar el propio archivo PKCS12). La extensión del archivo [!DNL .pfx] se utiliza comúnmente para archivos que admiten este formato.

>[!NOTE]
>
>El Adobe recomienda utilizar un HSM para una máxima seguridad.
>
>Consulte la *Directrices de implementación segura de Adobe Primetime DRM* guía.

>[!NOTE]
>
>A partir de Java 1.7, Sun Java de 64 bits para Windows ya no es compatible con las interfaces PKCS11 que Primetime DRM requiere para la comunicación con dispositivos HSM. Si planea utilizar un HSM, debe utilizar una versión de 32 bits de Java o utilizar un JDK que admita las interfaces PKCS11 completas.

Puede mantener una clave privada en un HSM y utilizar el SDK de DRM de Primetime para pasar las credenciales que obtiene del HSM. Si desea utilizar una credencial almacenada en un HSM, debe utilizar un proveedor JCE que pueda comunicarse con un HSM para obtener un identificador para la clave privada. A continuación, debe pasar el identificador de clave privada, el nombre del proveedor y el certificado que incluye la clave pública a `ServerCredentialFactory.getServerCredential()`.

El proveedor SunPKCS11 representa un ejemplo de proveedor JCE que puede utilizar para acceder a una clave privada en un HSM. Algunos HSM también se incluyen con un SDK de Java empaquetado con un proveedor JCE.

Consulte la documentación de Sun Java para obtener instrucciones sobre cómo utilizar este proveedor.

PEM y DER son formas de codificar un certificado de clave pública. PEM es una codificación en base 64 y DER es una codificación binaria. Los archivos de certificado suelen utilizar la extensión [!DNL .cer], [!DNL .pem], o [!DNL .der]. Los certificados se utilizan donde solo se requiere una clave pública. Si un componente solo requiere la clave pública para funcionar, se recomienda que proporcione ese componente con el certificado en lugar de una credencial o archivo PKCS12.
