---
description: El código puede solicitar una clave a través de DRMManager.
seo-description: El código puede solicitar una clave a través de DRMManager.
seo-title: Flujo de trabajo de solicitud de clave en HTML5 TVSDK
title: Flujo de trabajo de solicitud de clave en HTML5 TVSDK
uuid: a1f50eba-4301-49a1-b2e5-9add6687cff8
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Flujo de trabajo de solicitud de clave en HTML5 TVSDK{#key-request-workflow-on-html-tvsdk}

El código puede solicitar una clave a través de DRMManager.

El TVSDK del explorador también expone una API setProtectionData a través del objeto DRMManager:

```
[  /** 
   * This will only work for MSE. 
   * <p> Attach key system specific data to use for DRM 
license acquisition. </p> 
   * @param {Object} protectionData - an object containing property names corresponding to key system name strings 
   * (e.g. "org.w3.clearkey") and associated values being instances of 
   * MediaPlayer.vo.protection.ProtectionData. 
   * @returns {AdobePSDK.PSDKErrorCode} kECSuccess or one of the error codes. 
   * @function 
   * @memberof AdobePSDK.DRMManager# 
   */ 
   setProtectionData: function(protectionData) 
```

El código debería llamar a esta API antes de iniciar la reproducción del contenido de la forma normal. MediaPlayer.vo.protection.ProtectionData está documentada aquí: [https://vm2.dashif.org/dash.js/docs/jsdocs/MediaPlayer.vo.protection.ProtectionData.html](https://vm2.dashif.org/dash.js/docs/jsdocs/MediaPlayer.vo.protection.ProtectionData.html)

A continuación se muestra un objeto de datos de protección de muestra con direcciones URL de servidor de licencias tanto para PlayReady como para Widevine.

```
var protectionData = { 
   "com.widevine.alpha": { 
                          "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/ 
                           ?ExpressPlayToken=AQAAABIDKA4AAABQuPPoebWWZZD2l3APRKkkagEDOXm 
                           CjgbhsqJTYeZ9KabkjCvSLvuXGHiVLymBnouGXDdCKpbz5IvB3jCZp9U05pys 
                           l9eavucsWXnA0tafbM-1SSJKXOa70kvxAJ_ybhdcmy7-6g" 
                          }, 
   "com.microsoft.playready": { 
                               "serverURL": "https://expressplay-licensing.axprod.net/ 
                                LicensingService.ashx?ExpressPlayToken=AQAAAw_ZXqcAAAB 
                                gHD1gnn_AMQJKfFCP3k9zbBw2srzBLryJVLXclnjhcSBCz4TBzrtfe 
                                gmSw1hAKdFHTNL-KVBGsI4ygBnfPRBUCvGsVOwpQ944fhq45W06ygJ 
                                roB2xOrM03tbkWcrthI7y_UQdHzufHjcBqKZm8QDoqKpxrxc" 
                               } 
   };
```

TVSDK no proporciona ninguna API para forzar un sistema DRM en particular, ya que cada navegador solo admite un sistema DRM.
