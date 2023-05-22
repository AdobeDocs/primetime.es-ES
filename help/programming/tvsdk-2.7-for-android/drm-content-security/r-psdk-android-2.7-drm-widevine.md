---
description: Puede utilizar la DRM nativa de Android Widevine con flujos DASH.
title: DRM de Widevine
exl-id: 6a011cd7-446a-4f3a-ae36-110618001bf3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
