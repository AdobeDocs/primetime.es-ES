---
description: Puede completar flujos de trabajo específicos de Digital Rights Management (DRM).
seo-description: Puede completar flujos de trabajo específicos de Digital Rights Management (DRM).
seo-title: Administración de derechos digitales
title: Administración de derechos digitales
uuid: 011605c7-50c4-4ad5-9961-8cd92d0e6fd8
translation-type: tm+mt
source-git-commit: 5a786d8001326f874a51d65b8e8badca44f46e96

---


# Administración de derechos digitales {#digital-rights-management}

Puede completar flujos de trabajo específicos de Digital Rights Management (DRM).

Puede escuchar el `AdobePSDK.DRMMetadataInfoEvent` evento para controlar los flujos de trabajo de DRM:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## Agregar administración de derechos digitales {#add-digital-rights-management}

1. Agregue el `DRMMetadataInfoAvailableEvent` para obtener el `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. Implemente la `onDRMMetadataInfoAvailable` sección sobre la línea en el paso 1.

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

1. Cree DRMManager en el método setupVideo.

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

1. Cambie la URL del recurso a una secuencia de prueba DASH.

   >[!TIP]
   >
   >Asegúrese de actualizar el tipo de recurso, ya que ahora es DASH.

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. Pruebe la configuración.