---
description: El código de cliente pasa datos a una API de Android.
title: Flujo de trabajo de solicitud de clave en el PSDK de Android
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Flujo de trabajo de solicitud de clave en el SDK para Android{#key-request-workflow-on-android-psdk}

El código de cliente pasa datos a una API de Android.

En Android, el código de cliente debe pasar la URL del servidor de licencias y los datos de adquisición de licencias correspondientes mediante la siguiente API:

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

Después de llamar correctamente a esta API, su código puede iniciar la reproducción del contenido de la forma habitual. Si utiliza Expressplay, puede pasar el token como parte de la URL del servidor de licencias o como una propiedad de solicitud y eliminar el token de la URL del servidor de licencias.

Algunos dispositivos Android admiten tanto Widevine como PlayReady. En estos dispositivos, es posible que el cliente desee forzar al PSDK a descifrar el contenido mediante un DRM determinado si el contenido tiene varios encabezados DRM. Esto se puede hacer llamando a la siguiente API antes de la reproducción:

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

