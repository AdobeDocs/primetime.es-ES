---
description: Puede utilizar la DRM nativa de Android Widevine con flujos DASH.
seo-description: Puede utilizar la DRM nativa de Android Widevine con flujos DASH.
seo-title: DRM amplio
title: DRM amplio
uuid: ceb2f18f-9e53-47d6-9d4b-7004ac1d22c9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---


# DRM {#widevine-drm} Widevine

Puede utilizar la DRM nativa de Android Widevine con flujos DASH.

Llame a la siguiente API `com.adobe.mediacore.drm.DRMManager` antes de iniciar la reproducción:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argumentos:

* `drm` -  `"com.widevine.alpha"` para Widevine.

* `licenseServerURL` - Dirección URL del servidor de licencias Widevine que recibe solicitudes de licencia.
* `requestProperties` - Contiene encabezados adicionales para incluirlos en la solicitud de licencia saliente.

Por ejemplo, al usar contenido empaquetado para Expresiones DRM, utilice el siguiente código antes de reproducir:

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```

