---
description: Puede utilizar la DRM nativa de Android Widevine con flujos DASH.
title: DRM de Widevine
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# DRM de Widevine {#widevine-drm}

Puede utilizar la DRM nativa de Android Widevine con flujos DASH.

Realice una llamada a lo siguiente `com.adobe.mediacore.drm.DRMManager` API antes de iniciar la reproducción:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argumentos:

* `drm` - `"com.widevine.alpha"` para Widevine.

* `licenseServerURL` : URL del servidor de licencias de Widevine que recibe las solicitudes de licencia.
* `requestProperties` : contiene encabezados adicionales para incluirlos en la solicitud de licencia saliente.

Por ejemplo, cuando utilice contenido empaquetado para Expressplay DRM, utilice el siguiente código antes de reproducir:

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```
