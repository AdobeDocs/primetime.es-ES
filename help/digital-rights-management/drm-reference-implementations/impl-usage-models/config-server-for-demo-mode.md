---
title: Configurar el modo de demostración del modelo de uso
description: Configurar el modo de demostración del modelo de uso
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Configurar el modo de demostración del modelo de uso{#configure-usage-model-demo-mode}

Para que el servidor de implementación de referencia pueda emitir licencias para la demostración del modelo de uso, debe configurar el servidor para especificar cómo se generan las licencias para cada uno de los cuatro modelos de uso. Esto significa que debe especificar una directiva DRM para cada modelo de uso. La implementación de referencia incluye las siguientes políticas de DRM de muestra en el directorio [!DNL Reference Implementation/Server/Reference Implementation Server/resources/]:

* `dto-policy.pol` - (De Descargar En Propio)
* `vod-policy.pol` - (Alquiler/Vídeo bajo demanda)
* `sub-policy.pol` - (suscripción)
* `ad-policy.pol` - (Con financiación de publicidad)

>[!NOTE]
>
>Puede sustituir estas políticas de muestra por sus propias políticas de DRM.

1. Establezca estas propiedades en [!DNL flashaccess-refimpl.properties] para especificar la política de DRM que planea aplicar a cada modelo de uso:

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
