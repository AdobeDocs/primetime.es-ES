---
title: Opciones de empaquetado
description: Opciones de empaquetado
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Opciones de empaquetado{#packaging-options}

Hay muchas opciones disponibles para empaquetar contenido. Puede especificar las opciones en la variable `DRMParameters` e implementar las clases que pueden interactuar. Con estas clases puede establecer parámetros de firma y clave, así como indicar si se debe cifrar contenido de audio, contenido de vídeo o datos de secuencias de comandos. Para ver cómo se implementan en la implementación de referencia, consulte las descripciones de las opciones de línea de comandos de Media Packager que se describen en *Uso de las implementaciones de referencia de DRM de Adobe Primetime*. Estas opciones se basan en la API de Java y, por lo tanto, están disponibles para su uso mediante programación.

Las opciones de empaquetado incluyen:

* Opciones de cifrado (audio, vídeo, cifrado parcial).
* URL del servidor de licencias que el cliente utiliza como URL base para todas las solicitudes que se envían al servidor de licencias
* Certificado de transporte del servidor de licencias
* Certificado del servidor de licencias, utilizado para cifrar el CEK
* Credencial del empaquetador para firmar metadatos
