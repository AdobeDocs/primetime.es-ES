---
seo-title: Información general sobre la implementación de certificados
title: Información general sobre la implementación de certificados
uuid: e6413f9f-69a5-4881-bb13-47a80cf32a48
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Información general {#deploy-certificates-overview}

Para agregar certificados a los archivos de propiedades de Adobe Primetime DRM, convierta el archivo PKCS#7 a un archivo PFX con la clave privada y genere un archivo PEM o DER.

* Cuando se requiere una credencial (certificado y clave privada), las herramientas de línea de comandos de DRM de Primetime y el empaquetador de HTTP Dynamic Streaming de Adobe requieren un archivo PFX. El SDK, la implementación de referencia y Primetime DRM Server para flujo protegido pueden aceptar un archivo PFX y también pueden utilizar una credencial almacenada en un HSM.
* Cuando solo se requiere un certificado, la mayoría de los componentes de Primetime DRM pueden utilizar un archivo PEM, un archivo DER o un certificado en un HSM. El empaquetador de Adobe HTTP Dynamic Streaming solo acepta archivos DER para certificados.