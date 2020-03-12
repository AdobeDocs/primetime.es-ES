---
description: Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de la selección creativa de anuncios en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los elementos creativos de publicidad.
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de la selección creativa de anuncios en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los elementos creativos de publicidad.
seo-title: Actualización de las reglas de selección creativa de publicidad
title: Actualización de las reglas de selección creativa de publicidad
uuid: fddc5593-db40-4b03-bd7e-4b5fe5b6f650
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Información general {#update-ad-creative-selection-rules-overview}

Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de la selección creativa de anuncios en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los elementos creativos de publicidad.

Cuando el reproductor de vídeo realiza una solicitud a un servidor de publicidad, la respuesta VAST/VMAP suele incluir varios elementos creativos de publicidad ( `MediaFile` elementos), cada uno de los cuales proporciona una dirección URL a una versión diferente del códec de contenedor. En algunos casos, los creativos de anuncios de la respuesta VAST/VMAP proporcionan una velocidad de bits diferente para el anuncio. Si desea especificar su propia prioridad y reglas de transformación para estos elementos creativos de publicidad, puede hacerlo en el archivo de configuración [!DNL AdobeTVSDKConfig.json] .

>[!IMPORTANT]
>
>* No cambie el nombre del archivo de configuración TVSDK. El nombre debe permanecer [!DNL AdobeTVSDKConfig.json].
>* Este archivo debe colocarse en la [!DNL assets/] carpeta del proyecto.
>* El cambio de pistas de audio cuando se está reproduciendo un anuncio no cambia la pista de audio. Un reproductor no debe permitir que los usuarios cambien la pista de audio cuando se esté reproduciendo un anuncio.
>



Puede especificar dos tipos de reglas en [!DNL AdobeTVSDKConfig.json]: Reglas de *prioridad* y reglas de *normalización* .

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

Las reglas de publicidad se especifican mediante un archivo JSON. El formato del archivo JSON sigue siendo el mismo en ambas versiones del TVSDK. Sin embargo, en TVSDK v2.5, el archivo JSON de reglas de publicidad debe alojarse en una ubicación accesible mediante una URL HTTP. La aplicación puede utilizar una instancia de AuditudeSettings:

```
//TVSDK v2.5 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```

