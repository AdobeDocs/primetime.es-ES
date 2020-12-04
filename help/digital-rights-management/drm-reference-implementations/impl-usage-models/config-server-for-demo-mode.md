---
description: 'null'
seo-description: 'null'
seo-title: Configurar el modo de demostración del modelo de uso
title: Configurar el modo de demostración del modelo de uso
uuid: f818c7fc-e88f-4fa4-926e-08a1337b28d3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Configurar el modo de demostración del modelo de uso{#configure-usage-model-demo-mode}

Antes de que el servidor de implementación de referencia pueda emitir licencias para la demostración del modelo de uso, debe configurar el servidor para especificar cómo se generan las licencias para cada uno de los cuatro modelos de uso. Esto significa que debe especificar una directiva DRM para cada modelo de uso. La implementación de referencia incluye las siguientes directivas de DRM de muestra en el directorio [!DNL Reference Implementation/Server/Reference Implementation Server/resources/]:

* `dto-policy.pol` - (descarga propia)
* `vod-policy.pol` - (Alquiler/Video-On-Demand)
* `sub-policy.pol` - (Suscripción)
* `ad-policy.pol` - (Con financiación de publicidad)

>[!NOTE]
>
>Puede sustituir estas directivas de muestra por sus propias directivas de DRM.

1. Configure estas propiedades en [!DNL flashaccess-refimpl.properties] para especificar la directiva DRM que va a aplicar a cada modelo de uso:

   ```
   # DRM Policy file name for Download To Own usage 
   RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol 
   # DRM Policy file name for Rental usage 
   RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol 
   # DRM Policy file name for Subscription usage 
   RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol 
   # DRM Policy file name for Ad Supported (free) usage 
   RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
   ```

1. Copie los archivos de directiva de ejemplo en el directorio que especifique en la propiedad `config.resourcesDirectory` en [!DNL flashaccess-refimpl.properties].
