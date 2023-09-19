---
description: Puede utilizar el archivo de configuración de TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de selección de creatividad publicitaria en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los creativos de anuncios.
keywords: reglas de selección creativa;AdobeTVSDKConfig;agregar prioridades creativas;reglas de transformación
title: Actualizar reglas de selección de creatividad publicitaria
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Información general {#update-ad-creative-selection-rules-overview}

Puede utilizar el archivo de configuración de TVSDK (AdobeTVSDKConfig.json) para actualizar las prioridades de selección de creatividad publicitaria en las respuestas VAST/VMAP. También puede utilizar este archivo de configuración para definir las reglas de transformación de URL de origen para los creativos de anuncios.

Cuando el reproductor de vídeo realiza una solicitud a un servidor de publicidad, la respuesta de VAST/VMAP suele incluir varios elementos creativos de la publicidad ( `MediaFile` ), cada una de las cuales proporciona una dirección URL a una versión de códec contenedor diferente. En algunos casos, los creativos de anuncios en la respuesta VAST/VMAP proporcionan una velocidad de bits diferente para el anuncio. Si desea especificar su propia prioridad y reglas de transformación para estos anuncios creativos, puede hacerlo en la [!DNL AdobeTVSDKConfig.json] archivo de configuración.

>[!IMPORTANT]
>
>* No cambie el nombre del archivo de configuración de TVSDK. El nombre debe permanecer [!DNL AdobeTVSDKConfig.json].
>* Puede colocar este archivo en cualquier lugar que sea accesible para su paquete.
>

Puede especificar dos tipos de reglas en [!DNL AdobeTVSDKConfig.json]: *Prioridad* reglas y *Normalizar* reglas.

**[!UICONTROL Disabling Pre-Roll]**

Para deshabilitar el anuncio previo a la emisión, deberá cambiar los generadores de oportunidades predeterminados para que no realicen la llamada previa a la emisión. De forma predeterminada, TVSDK utiliza los siguientes generadores de oportunidades:

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

Para deshabilitar el anuncio previo a la emisión en directo, esto debería cambiar para incluir solo SpliceOutOpportunityGenerator:

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
