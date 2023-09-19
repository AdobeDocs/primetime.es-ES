---
description: La compatibilidad con el atributo withCredentials en XMLHttpRequests permite que las solicitudes de uso compartido de recursos de origen cruzado (CORS) incluyan las cookies del dominio de destino para una variedad de tipos de solicitud.
keywords: CORS;origen cruzado;uso compartido de recursos;cookies;con credenciales
title: Uso compartido de recursos de origen cruzado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Uso compartido de recursos de origen cruzado {#cross-origin-resource-sharing}

La compatibilidad con el atributo withCredentials en XMLHttpRequests permite que las solicitudes de uso compartido de recursos de origen cruzado (CORS) incluyan las cookies del dominio de destino para una variedad de tipos de solicitud.

Cuando el cliente solicita un manifiesto, segmento o clave, el servidor puede establecer una cookie que el cliente debe pasar para las solicitudes posteriores. Para permitir la lectura y escritura de cookies, el cliente debe establecer el `withCredentials` atribuir a `true` para solicitudes de origen cruzado.

Para habilitar `withCredentials` compatibilidad con la mayoría de los tipos de solicitudes al reproducir un recurso de medios determinado:

1. Cree el `CORSConfig` objeto.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Adjunte el `corsConfig` a la `NetworkConfiguration` objeto y conjunto `useCookieHeaderForAllRequests` hasta `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Establecer `networkConfig` en el `MediaPlayerItemConfig` objeto.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Aprobado `MediaPlayerItemConfig` a la `MediaPlayer.replaceCurrentResource` método.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>El `useCookieHeaderForAllRequests` El indicador no afecta a las solicitudes de licencia. Para establecer la variable `withCredentials` atribuir a `true` para una solicitud de licencia, debe configurar la variable `withCredentials` en sus datos de protección o especifique una clave de autorización en la variable `httpRequestHeaders` de sus datos de protección. Por ejemplo:

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

El indicador no afecta a una solicitud de licencia porque algunos servidores establecen el `Access-Control-Allow-Origin` de campo a comodín (&#39;&#42;&#39;) en su respuesta. Sin embargo, cuando el indicador de credenciales está establecido en `true`, el comodín no se puede usar en `Access-Control-Allow-Origin`. Si establece `useCookieHeaderForAllRequests` hasta `true` para todos los tipos de solicitudes, es posible que vea el siguiente error en una solicitud de licencia:

Recuerde la siguiente información:

* Cuando una llamada con `withCredentials=true` falla, TVSDK del explorador reintenta la llamada sin `withCredentials`.
* Cuando se realiza una llamada con `networkConfiguration.useCookieHeaderForAllRequests=false`, las solicitudes XHR se realizan sin el `withCredentials` atributo.
