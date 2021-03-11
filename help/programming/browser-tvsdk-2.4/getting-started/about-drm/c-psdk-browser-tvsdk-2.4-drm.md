---
description: Puede completar flujos de trabajo específicos del Digital Rights Management (DRM).
title: Digital Rights Management
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Digital Rights Management {#digital-rights-management}

Puede completar flujos de trabajo específicos del Digital Rights Management (DRM).

Puede escuchar el evento `AdobePSDK.DRMMetadataInfoEvent` para gestionar los flujos de trabajo de DRM:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## Agregar Digital Rights Management {#add-digital-rights-management}

1. Agregue `DRMMetadataInfoAvailableEvent` para obtener el `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. Implemente la sección `onDRMMetadataInfoAvailable` encima de la línea en el paso 1.

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

1. Cree DRMManager en el método setupVideo .

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

1. Agregue los datos de protección a drmManager.

   ```js
   drmManager.setProtectionData(protectionData);
   ```

1. Cambie la URL del recurso a un flujo de prueba DASH.

   >[!TIP]
   >
   >Asegúrese de actualizar el tipo de recurso, ya que ahora es DASH.

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. Pruebe la configuración.