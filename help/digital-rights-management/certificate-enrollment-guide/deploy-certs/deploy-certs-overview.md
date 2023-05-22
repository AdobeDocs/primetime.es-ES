---
title: Resumen de implementación de certificados
description: Resumen de implementación de certificados
copied-description: true
exl-id: 45a4bc7e-f987-4b9a-885d-d989d09566c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Información general {#deploy-certificates-overview}

Para añadir certificados a los archivos de propiedades DRM de Adobe Primetime, convierta el archivo PKCS#7 a un archivo PFX con la clave privada y genere un archivo PEM o un archivo DER.

* Cuando se requiere una credencial (certificado y clave privada), las herramientas de línea de comandos DRM de Primetime y el empaquetador de HTTP Dynamic Streaming de Adobe requieren un archivo PFX. El SDK, la implementación de referencia y el servidor DRM de Primetime para streaming protegido pueden aceptar un archivo PFX y también pueden utilizar una credencial almacenada en un HSM.
* Cuando solo se requiere un certificado, la mayoría de los componentes de DRM de Primetime pueden utilizar un archivo PEM, un archivo DER o un certificado en un HSM. El empaquetador de HTTP Dynamic Streaming de Adobe solo acepta archivos DER para certificados.
