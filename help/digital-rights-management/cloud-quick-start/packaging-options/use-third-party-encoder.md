---
title: Utilice un codificador de terceros
description: Utilice un codificador de terceros
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Utilice un codificador de terceros{#use-a-third-party-encoder}

Es posible que algunos clientes ya dispongan de una canalización de preparación de contenido mediante un codificador de vídeo (o Adobe Media Server) de hardware o software. En este caso, cualquier producto que pueda crear actualmente contenido protegido por DRM de Primetime puede empaquetar contenido para DRM de Primetime Cloud utilizando la misma configuración que el kit de protección DRM de Primetime Cloud. La información necesaria puede obtenerse de cualquiera de los ficheros de configuración existentes incluidos en el kit: [!DNL config_hls.xml] o [!DNL config_hds.xml].

Los elementos de configuración relevantes son:

* URL del servidor de licencias
* URL de servidor de claves
* Certificado de servidor de licencias
* Certificado de transporte
