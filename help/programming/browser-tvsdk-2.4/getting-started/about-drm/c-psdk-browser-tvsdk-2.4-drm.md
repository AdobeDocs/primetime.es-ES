---
description: Puede completar flujos de trabajo específicos del Digital Rights Management (DRM).
title: Digital Rights Management
exl-id: 5a40252b-2917-4341-bc64-8642432ddda9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Digital Rights Management {#digital-rights-management}

Puede completar flujos de trabajo específicos del Digital Rights Management (DRM).

Puede escuchar el `AdobePSDK.DRMMetadataInfoEvent` evento para gestionar flujos de trabajo de DRM:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## Añadir Digital Rights Management {#add-digital-rights-management}

1. Añada el `DRMMetadataInfoAvailableEvent` para obtener la `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. Implementación de `onDRMMetadataInfoAvailable` sección sobre la línea del paso 1.

   ```js
   var onDRMMetadataInfoAvaialble = function(event) { 
    var drmMetadataInfo = event.drmMetadataInfo; 
    var drmMetadata = null; 
   
    if(drmMetadataInfo) { 
     drmMetadata = drmMetadataInfo.drmMetadata; 
    } 
   
    drmManager.acquireLicense(drmMetadata, null, null); 
   };
   ```

1. Cree el Administrador de segmentos en el método setupVideo.

   ```js
   var drmManager = player.drmManager;
   ```

1. Cree los datos de protección para Widevine y PlayReady copiando el siguiente ejemplo:

   ```js
   var protectionData = { 
     "com.widevine.alpha":{ 
       "serverURL":"https://wv.service.expressplay.com/hms/wv/rights/? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]"  
     }, 
   
     "com.microsoft.playready":{ 
       "serverURL":"https://pr.test.expressplay.com/playready/RightsManager.asmx? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]", 
         "httpRequestHeaders":{ 
       } 
     } 
   };
   ```

1. Añada los datos de protección a drmManager.

   ```js
   drmManager.setProtectionData(protectionData);
   ```

1. Cambie la URL del recurso a un flujo de prueba DASH.

   >[!TIP]
   >
   >Asegúrese de actualizar el tipo de recurso, ya que ahora es GUIÓN.

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. Pruebe la configuración.
