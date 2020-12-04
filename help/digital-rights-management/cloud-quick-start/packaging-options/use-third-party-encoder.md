---
seo-title: Uso de un codificador de terceros
title: Uso de un codificador de terceros
uuid: 8649303c-b8e6-4c02-a8ad-5734af850bfe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Utilice un codificador de terceros{#use-a-third-party-encoder}

Es posible que algunos clientes ya dispongan de una canalización de preparación de contenido, mediante un codificador de vídeo de hardware o software (o Adobe Media Server). Si este es el caso, cualquier producto que pueda crear contenido protegido por DRM de Primetime puede empaquetar contenido para DRM de Primetime Cloud utilizando la misma configuración que el kit de protección DRM de Primetime Cloud. La información requerida puede obtenerse de cualquiera de los archivos de configuración existentes incluidos en el kit: [!DNL config_hls.xml] o [!DNL config_hds.xml].

Los elementos de configuración relevantes son:

* URL del servidor de licencias
* URL del servidor clave
* Certificado de servidor de licencias
* Certificado de transporte

