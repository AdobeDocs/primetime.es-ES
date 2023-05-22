---
description: Puede utilizar el archivo de configuración de TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de selección de creatividad publicitaria en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los creativos de anuncios.
title: Actualización y reglas de selección creativa
exl-id: 6664c120-2d4d-4cc0-8d9d-4bd8a66a5e88
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Información general {#updating-ad-creative-selection-rules}

Puede utilizar el archivo de configuración de TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de selección de creatividad publicitaria en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los creativos de anuncios.

Cuando el reproductor de vídeo realiza una solicitud a un servidor de publicidad, la respuesta de VAST/VMAP suele incluir varios elementos creativos de la publicidad ( `MediaFile` ), cada una de las cuales proporciona una dirección URL a una versión de códec contenedor diferente. En algunos casos, los creativos de anuncios en la respuesta VAST/VMAP proporcionan una velocidad de bits diferente para el anuncio. Si desea especificar su propia prioridad y reglas de transformación para estos anuncios creativos, puede hacerlo en la [!DNL AdobeTVSDKConfig.json] archivo de configuración.

>[!IMPORTANT]
>
>* No cambie el nombre del archivo de configuración de TVSDK. El nombre debe permanecer [!DNL AdobeTVSDKConfig.json].
>* Este archivo debe alojarse en la red de distribución de contenido (CDN).
>


Puede especificar dos tipos de reglas en [!DNL AdobeTVSDKConfig.json]: *Prioridad* reglas y *Normalizar* reglas.
