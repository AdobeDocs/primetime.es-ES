---
description: Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de selección creativa de publicidad en respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los creativos de anuncios.
keywords: reglas de selección creativa;AdobeTVSDKConfig;prioridades creativas de publicidad;reglas de transformación
title: Actualizar las reglas de selección creativa de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Información general {#update-ad-creative-selection-rules-overview}

Puede utilizar el archivo de configuración TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de selección creativa de publicidad en respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los creativos de anuncios.

Cuando el reproductor de vídeo realiza una solicitud a un servidor de publicidad, la respuesta VAST/VMAP suele incluir varios elementos creativos de publicidad ( `MediaFile` elementos), cada uno de los cuales proporciona una URL a una versión diferente del códec contenedor. En algunos casos, los creativos de anuncios en la respuesta VAST/VMAP proporcionan una velocidad de bits diferente para el anuncio. Si desea especificar sus propias reglas de prioridad y transformación para estos creativos de publicidad, puede hacerlo en el archivo de configuración [!DNL AdobeTVSDKConfig.json] .

>[!IMPORTANT]
>
>* No cambie el nombre del archivo de configuración de TVSDK. El nombre debe permanecer [!DNL AdobeTVSDKConfig.json].
>* Puede colocar este archivo en cualquier parte accesible para su paquete.

>



Puede especificar dos tipos de reglas en [!DNL AdobeTVSDKConfig.json]: Reglas *Priority* y reglas *Normalizar*.

**[!UICONTROL Disabling Pre-Roll]**

Para desactivar el anuncio previo a la emisión, deberá cambiar los generadores de oportunidades predeterminados para que no realice la llamada previa a la emisión. De forma predeterminada, TVSDK utiliza los siguientes generadores de oportunidades:

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

Para desactivar el anuncio previo a la emisión en directo, esto debería cambiar para incluir solo el SpliceOutOportunityGenerator:

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

