---
description: El código de cliente pasa datos a una API de Android.
title: Flujo de trabajo de solicitud de claves en Android PSDK
exl-id: 3ff52c0d-0789-4fe5-bf9d-f03184bad488
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Flujo de trabajo de solicitud de claves en Android PSDK{#key-request-workflow-on-android-psdk}

El código de cliente pasa datos a una API de Android.

En Android, el código de cliente debe pasar la URL del servidor de licencias y los datos de adquisición de licencias adjuntos mediante la siguiente API:

```
class DRMManager 
   { 
   ... 
   /* 
   * Set the license server URL and attached request properties that the PSDK should use for the passed in drm type.  
   * 
   * drmType: "com.widevine.alpha" for widevine. "com.microsoft.playready" for playready. 
   * licenseServerURL: self explanatory.  
   * requestProperties: key value pairs to be attached as HTTP headers to all license request sent to the passed in license server URL. Pass in 
   * NULL if none is needed.  
   */ 
   public static void setProtectionData(String drmType, String licenseServerURL,  Map<String, String> requestProperties); 
    }
```

Después de llamar correctamente a esta API, el código puede iniciar la reproducción del contenido de la manera habitual. Si utiliza Expressplay, puede pasar el token como parte de la URL del servidor de licencias o como una propiedad de solicitud y eliminar el token de la URL del servidor de licencias.

Algunos dispositivos Android son compatibles con Widevine y PlayReady. En estos dispositivos, es posible que el cliente desee obligar a PSDK a descifrar el contenido mediante un DRM concreto si el contenido tiene varios encabezados DRM. Esto se puede hacer llamando a la siguiente API antes de la reproducción:

```
class MediaPlayer 
   { 
   ... 
    
   /* 
   * drm: pass in "com.widevine.alpha" for widevine or "com.microsoft.playready" for playready 
   * 
   */ 
   public void setDRMScheme(String drm) throws MediaPlayerException 
   }
```
