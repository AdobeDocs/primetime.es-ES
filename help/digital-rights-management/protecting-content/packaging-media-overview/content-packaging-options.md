---
seo-title: Opciones de paquete
title: Opciones de paquete
uuid: 04244428-cb42-438a-8f16-91532c70ea60
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# Opciones de paquete{#packaging-options}

Existen numerosas opciones disponibles para empaquetar contenido. Puede especificar las opciones en la interfaz `DRMParameters` e implementar las clases que pueden interactuar. Con estas clases puede definir parámetros de firma y clave, así como también indicar si desea cifrar contenido de audio, vídeo o datos de secuencias de comandos. Para ver cómo se implementan en la implementación de referencia, consulte las descripciones de las opciones de línea de comandos de Media Packager que se describen en *Uso de las implementaciones de referencia de Adobe Primetime DRM*. Estas opciones se basan en la API de Java y, por lo tanto, están disponibles para el uso programático.

Las opciones de empaquetado incluyen:

* Opciones de codificación (audio, vídeo, cifrado parcial).
* URL del servidor de licencias que el cliente utiliza como URL base para todas las solicitudes que se envían al servidor de licencias
* Certificado de transporte del servidor de licencias
* Certificado de servidor de licencias, utilizado para cifrar el CEK
* Credenciales de Packager para firmar metadatos

