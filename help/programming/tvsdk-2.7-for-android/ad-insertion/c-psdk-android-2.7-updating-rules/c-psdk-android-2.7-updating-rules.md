---
description: Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de selección creativa de publicidad en respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los creativos de anuncios.
keywords: reglas de selección creativa;AdobeTVSDKConfig;prioridades creativas de publicidad;reglas de transformación
title: Actualizar las reglas de selección creativa de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# Información general {#update-ad-creative-selection-rules-overview}

Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de selección creativa de publicidad en respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los creativos de anuncios.

Cuando el reproductor de vídeo realiza una solicitud a un servidor de publicidad, la respuesta VAST/VMAP suele incluir varios elementos creativos de publicidad ( `MediaFile` elementos), cada uno de los cuales proporciona una URL a una versión diferente del códec contenedor. En algunos casos, los creativos de anuncios en la respuesta VAST/VMAP proporcionan una velocidad de bits diferente para el anuncio. Si desea especificar sus propias reglas de prioridad y transformación para estos creativos de publicidad, puede hacerlo en el archivo de configuración [!DNL AdobeTVSDKConfig.json] .

>[!IMPORTANT]
>
>* No cambie el nombre del archivo de configuración de TVSDK. El nombre debe permanecer [!DNL AdobeTVSDKConfig.json].
>* Este archivo debe colocarse en la carpeta [!DNL assets/] del proyecto.
>* Cambiar las pistas de audio cuando se reproduce el anuncio no cambia la pista de audio. Un reproductor no debe permitir a los usuarios cambiar la pista de audio cuando se reproduce un anuncio.

>



Puede especificar dos tipos de reglas en [!DNL AdobeTVSDKConfig.json]: Reglas *Priority* y reglas *Normalizar*.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

Las reglas de publicidad se especifican usando un archivo JSON. El formato del archivo JSON sigue siendo el mismo en ambas versiones de TVSDK. Sin embargo, en TVSDK v2.5, el archivo JSON de reglas de publicidad debe alojarse en una ubicación accesible a través de una URL HTTP. La aplicación puede utilizar una instancia de AuditudeSettings:

```
//TVSDK v2.5 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```

