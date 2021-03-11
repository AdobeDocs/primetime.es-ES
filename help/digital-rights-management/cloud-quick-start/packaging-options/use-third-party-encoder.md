---
title: Uso de un codificador de terceros
description: Uso de un codificador de terceros
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Usar un codificador de terceros{#use-a-third-party-encoder}

Es posible que algunos clientes ya tengan una canalización de preparación de contenido implementada, mediante un codificador de vídeo de hardware o software (o Adobe Medium Server). En este caso, cualquier producto que pueda crear contenido protegido por DRM de Primetime puede empaquetar contenido para DRM de Primetime Cloud utilizando los mismos ajustes de configuración que el Kit de protección DRM de Primetime Cloud. La información requerida puede obtenerse de cualquiera de los archivos de configuración existentes incluidos en el kit: [!DNL config_hls.xml] o [!DNL config_hds.xml].

Los elementos de configuración relevantes son:

* URL del servidor de licencias
* URL del servidor de claves
* Certificado de servidor de licencias
* Certificado de transporte

