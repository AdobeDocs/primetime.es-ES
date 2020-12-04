---
description: Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de la selección creativa de anuncios en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los elementos creativos de publicidad.
seo-description: Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de la selección creativa de anuncios en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los elementos creativos de publicidad.
seo-title: Actualización de las reglas de selección creativa de publicidad
title: Actualización de las reglas de selección creativa de publicidad
uuid: 9eb4ccc2-425f-4c01-a095-f2043df4e25c
translation-type: tm+mt
source-git-commit: 6837c753b2f031b024ff510cda670340f346c4e1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# Información general {#updating-ad-creative-selection-rules}

Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de la selección creativa de anuncios en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los elementos creativos de publicidad.

Cuando el reproductor de vídeo realiza una solicitud a un servidor de publicidad, la respuesta VAST/VMAP suele incluir varios elementos creativos de publicidad ( `MediaFile` elementos), cada uno de los cuales proporciona una dirección URL a una versión diferente del códec de contenedor. En algunos casos, los creativos de anuncios de la respuesta VAST/VMAP proporcionan una velocidad de bits diferente para el anuncio. Si desea especificar sus propias reglas de prioridad y transformación para estos elementos creativos de publicidad, puede hacerlo en el archivo de configuración [!DNL AdobeTVSDKConfig.json].

>[!IMPORTANT]
>
>* No cambie el nombre del archivo de configuración TVSDK. El nombre debe permanecer [!DNL AdobeTVSDKConfig.json].
>* Este archivo debe alojarse en la red de envío de contenido (CDN).

>



Puede especificar dos tipos de reglas en [!DNL AdobeTVSDKConfig.json]: *Prioridad* y *Normalizar* reglas.
