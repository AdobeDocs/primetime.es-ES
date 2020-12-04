---
description: Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de la selección creativa de anuncios en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los elementos creativos de publicidad.
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de la selección creativa de anuncios en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los elementos creativos de publicidad.
seo-title: Actualización de las reglas de selección creativa de publicidad
title: Actualización de las reglas de selección creativa de publicidad
uuid: c33fe1f0-78cb-4dc2-89d2-e9fb1bf0e73f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Información general {#update-ad-creative-selection-rules-overview}

Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de la selección creativa de anuncios en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los elementos creativos de publicidad.

Cuando el reproductor de vídeo realiza una solicitud a un servidor de publicidad, la respuesta VAST/VMAP suele incluir varios elementos creativos de publicidad ( `MediaFile` elementos), cada uno de los cuales proporciona una dirección URL a una versión diferente del códec de contenedor. En algunos casos, los creativos de anuncios de la respuesta VAST/VMAP proporcionan una velocidad de bits diferente para el anuncio. Si desea especificar sus propias reglas de prioridad y transformación para estos elementos creativos de publicidad, puede hacerlo en el archivo de configuración [!DNL AdobeTVSDKConfig.json].

>[!IMPORTANT]
>
>* No cambie el nombre del archivo de configuración TVSDK. El nombre debe permanecer [!DNL AdobeTVSDKConfig.json].
>* Puede colocar este archivo en cualquier lugar al que pueda acceder el paquete.

>



Puede especificar dos tipos de reglas en [!DNL AdobeTVSDKConfig.json]: *Prioridad* y *Normalizar* reglas.

**[!UICONTROL Disabling Pre-Roll]**

Para desactivar el prelanzamiento, deberá cambiar los generadores de oportunidades predeterminados para que no realicen la llamada previa. De forma predeterminada, TVSDK utiliza los siguientes generadores de oportunidades:

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    result.push(new AdSignalingModeOpportunityGenerator()); 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
} 
```

Para desactivar el prelanzamiento en los flujos en directo, esto debería cambiar para incluir solo SpliceOutOpportunityGenerator:

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    if (preroll_enabled == true) { 
        result.push(new AdSignalingModeOpportunityGenerator()); 
    } 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
}
```

