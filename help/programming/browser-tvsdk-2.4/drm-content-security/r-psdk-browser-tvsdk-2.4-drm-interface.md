---
description: Browser TVSDK proporciona una interfaz DRM que puede utilizar para reproducir contenido protegido por diferentes soluciones DRM, incluidas FairPlay, PlayReady y Widevine.
title: Descripción general de la interfaz DRM
exl-id: aa13f042-4472-4fc3-b7ba-61746b8e024a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Descripción general de la interfaz DRM{#drm-interface-overview}

Browser TVSDK proporciona una interfaz DRM que puede utilizar para reproducir contenido protegido por diferentes soluciones DRM, incluidas FairPlay, PlayReady y Widevine.

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>La compatibilidad con DRM está disponible para flujos MPEG-Dash protegidos con sistemas DRM Microsoft PlayReady (en Internet Explorer en Windows 8.1 y Edge) y Widevine (en Google Chrome). La compatibilidad con DRM está disponible para emisiones HLS en Safari protegidas con FairPlay.

La interfaz clave del flujo de trabajo de DRM es `DRMManager`. Una referencia a la `DRMManager` se puede obtener a través de la instancia de MediaPlayer:

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

Este es un flujo de trabajo de alto nivel para la reproducción de contenido protegido por DRM:

1. Para adjuntar los datos específicos del sistema DRM que utilizará el TVSDK del explorador en el proceso de adquisición de licencia para un flujo protegido, realice la siguiente llamada antes de invocar `mediaPlayer.replaceCurrentResource`:

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
          "serverURL": { 
             "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
             "license-request": "https://example.com:8096/flashaccess/req", 
             "license-release": "https://example.com:8096/flashaccess/req" 
          }, 
          "httpRequestHeaders": { 
          } 
       } 
   }; 
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. Si se espera que el mismo contenido funcione con distintos sistemas DRM en distintos navegadores, se pueden especificar datos de protección para varios sistemas DRM.

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
           "serverURL": { 
               "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
               "license-request": "https://example.com:8096/flashaccess/req", 
               "license-release": "https://example.com:8096/flashaccess/req" 
           }, 
           "httpRequestHeaders": { 
           } 
       }, 
       "com.widevine.alpha": { 
           "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "dt-custom-data": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.microsoft.playready": { 
           "serverURL": "https://pr.test.expressplay.com/playready/RightsManager.asmx?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "http-header-CustomData": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.apple.fps.1_0": { 
           "serverURL": "https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<token value>", 
           "certificateURL": "Path_To_certificate.cer", 
           "licenseResponseType": "arraybuffer", 
           "httpRequestHeaders": { 
               "Content-type": "application/octet-stream" 
           } 
       }, 
       "org.w3.clearkey": { 
           "clearkeys": { 
               "H3JbV93QV3mPNBKQON2UtQ": "ClKhDPHMtCouEx1vLGsJsA", 
               "IAAAACAAIAAgACAAAAAAAg": "5t1CjnbMFURBou087OSj2w" 
           } 
       } 
   }; 
   
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. Cuando no se configuran datos de protección, se recupera la información necesaria, como la URL de la licencia, del cuadro PSSH para los sistemas DRM, cuando corresponda.

   >[!TIP]
   >
   >Al especificar los datos de protección, se anula la URL de licencia especificada en el cuadro PSSH.

1. De forma predeterminada, el tipo de sesión de la licencia DRM es temporal, lo que significa que la licencia no se almacena después de cerrar la sesión.

   Puede especificar un tipo de sesión mediante una API en `DRMManager`.  Para la compatibilidad con versiones anteriores, los tipos de sesión incluyen `temporary`, `persistent-license`, `persistent-usage-record`, y `persistent`.

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. Si la variable `sessionType` se utiliza es `persistent-license` o `persistent`, la licencia DRM se puede devolver invocando `DRMManager.returnLicense`.

   ```js
   var onLicenseReturnFunc = function () { 
       console.log("DRM: License Return Complete "); 
   }, 
   
   onLicenseReturnErrorFunc = function (major, minor, errorString/*, errorServerUrl*/) { 
      console.log("DRM: License Return Error: " + errorString); 
   }, 
   
   drmManager = mediaPlayer.drmManager; 
   
   if (drmManager) { 
       var returnLicenseListener = new  
           AdobePSDK.DRMReturnLicenseListener(onLicenseReturnFunc, onLicenseReturnErrorFunc); 
       drmManager.returnLicense(null, null, null, false, returnLicenseListener, drmLicense.session); 
   }
   ```
