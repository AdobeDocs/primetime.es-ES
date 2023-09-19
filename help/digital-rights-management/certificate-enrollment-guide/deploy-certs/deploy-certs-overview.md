---
title: Resumen de implementación de certificados
description: Resumen de implementación de certificados
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Información general {#deploy-certificates-overview}

Para añadir certificados a los archivos de propiedades DRM de Adobe Primetime, convierta el archivo PKCS#7 a un archivo PFX con la clave privada y genere un archivo PEM o un archivo DER.

* Cuando se requiere una credencial (certificado y clave privada), las herramientas de línea de comandos DRM de Primetime y el empaquetador de HTTP Dynamic Streaming de Adobe requieren un archivo PFX. El SDK, la implementación de referencia y el servidor DRM de Primetime para streaming protegido pueden aceptar un archivo PFX y también pueden utilizar una credencial almacenada en un HSM.
* Cuando solo se requiere un certificado, la mayoría de los componentes de DRM de Primetime pueden utilizar un archivo PEM, un archivo DER o un certificado en un HSM. El empaquetador de HTTP Dynamic Streaming de Adobe solo acepta archivos DER para certificados.
