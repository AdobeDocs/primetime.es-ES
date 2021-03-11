---
description: Puede utilizar el DRM nativo de Android Widevine con flujos DASH.
title: DRM Widevine
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# DRM {#widevine-drm} Widevine

Puede utilizar el DRM nativo de Android Widevine con flujos DASH.

Llame a la siguiente API `com.adobe.mediacore.drm.DRMManager` antes de comenzar la reproducción:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argumentos:

* `drm` -  `"com.widevine.alpha"` para Widevine.

* `licenseServerURL` - La URL del servidor de licencias Widevine que recibe solicitudes de licencia.
* `requestProperties` - Contiene encabezados adicionales para incluirlos en la solicitud de licencia saliente.

Por ejemplo, cuando utilice contenido empaquetado para Expressplay DRM, utilice el siguiente código antes de reproducir:

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```

