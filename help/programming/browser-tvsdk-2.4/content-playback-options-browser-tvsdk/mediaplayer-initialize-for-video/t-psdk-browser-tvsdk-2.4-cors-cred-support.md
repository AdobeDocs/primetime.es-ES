---
description: La compatibilidad con el atributo withCredentials en XMLHttpRequests permite que las solicitudes de uso compartido de recursos de origen cruzado (CORS) incluyan las cookies del dominio de destino para diversos tipos de solicitudes.
keywords: CORS;cross origin;resource sharing;cookies;withCredentials
seo-description: La compatibilidad con el atributo withCredentials en XMLHttpRequests permite que las solicitudes de uso compartido de recursos de origen cruzado (CORS) incluyan las cookies del dominio de destino para diversos tipos de solicitudes.
seo-title: Uso compartido de recursos de origen cruzado
title: Uso compartido de recursos de origen cruzado
uuid: e788b542-d4ac-48aa-91e2-1e88068cbba1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Uso compartido de recursos de origen cruzado {#cross-origin-resource-sharing}

La compatibilidad con el atributo withCredentials en XMLHttpRequests permite que las solicitudes de uso compartido de recursos de origen cruzado (CORS) incluyan las cookies del dominio de destino para diversos tipos de solicitudes.

Cuando el cliente solicita un manifiesto, segmento o clave, el servidor puede establecer una cookie que el cliente debe pasar para solicitudes posteriores. Para permitir la lectura y escritura de cookies, el cliente debe establecer el `withCredentials` atributo en `true` para solicitudes de origen cruzado.

Para habilitar `withCredentials` la compatibilidad con la mayoría de los tipos de solicitudes al reproducir un recurso de medios determinado:

1. Cree el `CORSConfig` objeto.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Adjunte el `corsConfig` objeto al `NetworkConfiguration` objeto y defina `useCookieHeaderForAllRequests` en `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Se establece `networkConfig` en el `MediaPlayerItemConfig` objeto.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Pasa `MediaPlayerItemConfig` al `MediaPlayer.replaceCurrentResource` método.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>El `useCookieHeaderForAllRequests` indicador no afecta a las solicitudes de licencia. Para establecer el `withCredentials` atributo en `true` para una solicitud de licencia, debe configurar el `withCredentials` atributo en los datos de protección o especificar una clave de autorización en el contenido `httpRequestHeaders` de los datos de protección. Por ejemplo:

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

El indicador no afecta a una solicitud de licencia porque algunos servidores definen el `Access-Control-Allow-Origin` campo como comodín (&#39;*&#39;) en su respuesta. Sin embargo, cuando el indicador de credenciales está establecido en `true`, no se puede usar el comodín en `Access-Control-Allow-Origin`. Si establece `useCookieHeaderForAllRequests` en `true` para todos los tipos de solicitudes, puede que vea el siguiente error para una solicitud de licencia:

Recuerde la siguiente información:

* Cuando se produce un error en una llamada con `withCredentials=true` , el SDK de TVSDK del explorador reintenta la llamada sin `withCredentials`.
* Cuando se realiza una llamada con `networkConfiguration.useCookieHeaderForAllRequests=false`, las solicitudes XHR se realizan sin el `withCredentials` atributo .