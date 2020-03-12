---
description: Puede utilizar las funciones del sistema Primetime Digital Rights Management (DRM) para proporcionar un acceso seguro al contenido de vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como alternativa a la solución integrada de Adobe.
seo-description: Puede utilizar las funciones del sistema Primetime Digital Rights Management (DRM) para proporcionar un acceso seguro al contenido de vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como alternativa a la solución integrada de Adobe.
seo-title: DRM amplio
title: DRM amplio
uuid: 3a5fd786-4319-4e92-83b6-0f5328df6a44
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# DRM amplio {#widevine-drm}

Puede utilizar las funciones del sistema Primetime Digital Rights Management (DRM) para proporcionar un acceso seguro al contenido de vídeo. Como alternativa, puede utilizar soluciones DRM de terceros como alternativa a la solución integrada de Adobe.

Póngase en contacto con su representante de Adobe para obtener la información más actualizada sobre la disponibilidad de soluciones DRM de terceros.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

Puede utilizar la DRM nativa de Android Widevine con flujos DASH.

Llame a la siguiente `com.adobe.mediacore.drm.DRMManager` API antes de iniciar la reproducción:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argumentos:

* `drm` - `"com.widevine.alpha"` para Widevine.

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
