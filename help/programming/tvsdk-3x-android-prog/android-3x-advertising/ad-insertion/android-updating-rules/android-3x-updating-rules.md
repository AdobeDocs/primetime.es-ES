---
description: Puede utilizar el archivo de configuración de TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de selección de creatividad publicitaria en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los creativos de anuncios.
keywords: reglas de selección creativa;AdobeTVSDKConfig;agregar prioridades creativas;reglas de transformación
title: Actualizar reglas de selección de creatividad publicitaria
exl-id: da0420a0-6be9-47c8-bdd8-45f0f1860f28
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Información general {#update-ad-creative-selection-rules-overview}

Puede utilizar el archivo de configuración de TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de selección de creatividad publicitaria en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los creativos de anuncios.

Cuando el reproductor de vídeo realiza una solicitud a un servidor de publicidad, la respuesta de VAST/VMAP suele incluir varios elementos creativos de la publicidad ( `MediaFile` ), cada una de las cuales proporciona una dirección URL a una versión de códec contenedor diferente. En algunos casos, los creativos de anuncios en la respuesta VAST/VMAP proporcionan una velocidad de bits diferente para el anuncio. Si desea especificar su propia prioridad y reglas de transformación para estos anuncios creativos, puede hacerlo en la [!DNL AdobeTVSDKConfig.json] archivo de configuración.

>[!IMPORTANT]
>
>* No cambie el nombre del archivo de configuración de TVSDK. El nombre debe permanecer [!DNL AdobeTVSDKConfig.json].
>* Este archivo debe colocarse en la [!DNL assets/] de su proyecto.
>* El cambio de pistas de audio cuando se está reproduciendo un anuncio no cambia la pista de audio. Un reproductor no debe permitir a los usuarios cambiar la pista de audio cuando se reproduce un anuncio.
>


Puede especificar dos tipos de reglas en [!DNL AdobeTVSDKConfig.json]: *Prioridad* reglas y *Normalizar* reglas.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

Las reglas de publicidad se especifican mediante un archivo JSON. El formato del archivo JSON sigue siendo el mismo en ambas versiones de TVSDK. Sin embargo, en TVSDK v3.0, el archivo JSON de reglas de publicidad debe alojarse en una ubicación accesible a través de una URL HTTP. La aplicación puede utilizar una instancia de AuditudeSettings:

```
//TVSDK v3.0 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
