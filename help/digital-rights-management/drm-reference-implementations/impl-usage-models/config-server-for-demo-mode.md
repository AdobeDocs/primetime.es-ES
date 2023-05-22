---
title: Configurar el modo de demostración del modelo de uso
description: Configurar el modo de demostración del modelo de uso
copied-description: true
exl-id: 593acfbd-fd37-4bab-ac8e-5cb62963fac4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Configurar el modo de demostración del modelo de uso{#configure-usage-model-demo-mode}

Antes de que el servidor de implementación de referencia pueda emitir licencias para la demostración del modelo de uso, debe configurar el servidor para especificar cómo se generan las licencias para cada uno de los cuatro modelos de uso. Esto significa que debe especificar una política de DRM para cada modelo de uso. La Implementación de referencia incluye las siguientes políticas de DRM de ejemplo en la [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] directorio:

* `dto-policy.pol` - (Descarga por su cuenta)
* `vod-policy.pol` - (Alquiler/Vídeo a petición)
* `sub-policy.pol` - (Suscripción)
* `ad-policy.pol` - (Ad-financiado)

>[!NOTE]
>
>Puede sustituir estas políticas de ejemplo por sus propias políticas de DRM.

1. Establezca estas propiedades en [!DNL flashaccess-refimpl.properties] para especificar la política de DRM que se va a aplicar a cada modelo de uso:

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

1. Copie los archivos de directivas de ejemplo en el directorio especificado en la `config.resourcesDirectory` propiedad en [!DNL flashaccess-refimpl.properties].
