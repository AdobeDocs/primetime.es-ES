---
title: Información general sobre la implementación de certificados
description: Información general sobre la implementación de certificados
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Información general {#deploy-certificates-overview}

Para añadir certificados a los archivos de propiedades DRM de Adobe Primetime, convierta el archivo PKCS#7 a un archivo PFX con la clave privada y genere un archivo PEM o un archivo DER.

* Cuando se requiere una credencial (certificado y clave privada), las herramientas de línea de comandos de Primetime DRM y el empaquetador de HTTP Dynamic Streaming de Adobe requieren un archivo PFX. El SDK, la implementación de referencia y el servidor DRM de Primetime para la transmisión protegida pueden aceptar un archivo PFX y también pueden utilizar una credencial almacenada en un HSM.
* Cuando solo se requiere un certificado, la mayoría de los componentes de Primetime DRM pueden utilizar un archivo PEM, un archivo DER o un certificado en un HSM. El empaquetador de HTTP Dynamic Streaming de Adobe solo acepta archivos DER para certificados.