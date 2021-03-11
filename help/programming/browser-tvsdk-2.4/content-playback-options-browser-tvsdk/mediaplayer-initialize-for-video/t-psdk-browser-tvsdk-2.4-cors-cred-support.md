---
description: La compatibilidad con el atributo withCredentials en XMLHttpRequests permite que las solicitudes de uso compartido de recursos de origen diverso (CORS) incluyan las cookies del dominio de destino para varios tipos de solicitud.
keywords: CORS;origen cruzado;uso compartido de recursos;cookies;conCredentials
title: Uso compartido de recursos de origen diverso
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Uso compartido de recursos de origen diverso {#cross-origin-resource-sharing}

La compatibilidad con el atributo withCredentials en XMLHttpRequests permite que las solicitudes de uso compartido de recursos de origen diverso (CORS) incluyan las cookies del dominio de destino para varios tipos de solicitud.

Cuando el cliente solicita un manifiesto, segmento o clave, el servidor puede establecer una cookie que el cliente debe pasar para solicitudes posteriores. Para permitir la lectura y escritura de cookies, el cliente debe establecer el atributo `withCredentials` en `true` para las solicitudes de origen cruzado.

Para habilitar la compatibilidad con `withCredentials` para la mayoría de los tipos de solicitudes al reproducir un recurso de medios determinado:

1. Cree el objeto `CORSConfig`.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Adjunte `corsConfig` al objeto `NetworkConfiguration` y establezca `useCookieHeaderForAllRequests` en `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Establezca `networkConfig` en el objeto `MediaPlayerItemConfig`.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Pase `MediaPlayerItemConfig` al método `MediaPlayer.replaceCurrentResource`.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>El indicador `useCookieHeaderForAllRequests` no afecta a las solicitudes de licencia. Para establecer el atributo `withCredentials` en `true` para una solicitud de licencia, debe establecer el atributo `withCredentials` en los datos de protección o especificar una clave de autorización en el `httpRequestHeaders` de los datos de protección. Por ejemplo:

```
# Example 1 
{ 
    "com.widevine.alpha": {  
        "withCredentials":true,  
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i]" } 
} 
 
# Example 2 
{ 
    "com.widevine.alpha": { 
        "httpRequestHeaders": {  
            "authorization": "true"  
            }, 
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i>]" }
        } 
}
```

El indicador no afecta a una solicitud de licencia porque algunos servidores establecen el campo `Access-Control-Allow-Origin` como comodín (&#39;*&#39;) en su respuesta. Sin embargo, cuando el indicador de credenciales está establecido en `true`, el comodín no se puede usar en `Access-Control-Allow-Origin`. Si establece `useCookieHeaderForAllRequests` en `true` para todos los tipos de solicitudes, puede que vea el siguiente error para una solicitud de licencia:

Recuerde la siguiente información:

* Cuando falla una llamada con `withCredentials=true`, el SDK de TVSDK del explorador vuelve a intentar la llamada sin `withCredentials`.
* Cuando se realiza una llamada con `networkConfiguration.useCookieHeaderForAllRequests=false`, las solicitudes XHR se realizan sin el atributo `withCredentials`.