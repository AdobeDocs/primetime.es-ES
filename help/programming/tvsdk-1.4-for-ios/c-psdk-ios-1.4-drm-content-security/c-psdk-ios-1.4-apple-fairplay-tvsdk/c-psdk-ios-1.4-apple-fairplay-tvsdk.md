---
description: Para implementar FairPlay Streaming en su aplicación TVSDK, debe escribir un Resource Loader, que enviará una solicitud de adquisición de licencia a su servidor FairPlay Streaming.
title: Apple FairPlay en aplicaciones TVSDK
exl-id: 83fdc75b-f736-4091-ab80-e7f6e9723482
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Apple FairPlay en aplicaciones TVSDK  {#apple-fairplay-in-tvsdk-applications}

Para implementar FairPlay Streaming en su aplicación TVSDK, debe escribir un Resource Loader, que enviará una solicitud de adquisición de licencia a su servidor FairPlay Streaming.

El código del cargador de recursos es responsable de las siguientes tareas:

1. Determine dónde enviar la solicitud de adquisición de licencia.
1. Dé formato a la solicitud.
1. Proporcione la información necesaria al servidor para que este pueda decidir si se debe permitir la solicitud.

Por ejemplo, si utiliza la DRM de Adobe de Primetime Cloud con tecnología ExpressPlay, el cargador de recursos envía la solicitud a:

```
https://fp-gen.service.expressplay.com
```

El cargador de recursos da formato a la solicitud y adjunta un token de ExpressPlay que autoriza la reproducción en la dirección URL. Al adquirir el token de ExpressPlay, hay varias opciones que se deben tener en cuenta. Estas opciones están determinadas por la forma en que empaquetó el contenido.

Al empaquetar el contenido, el empaquetador inserta lo siguiente `skd:` URL en su manifiesto M3U8. Después del `skd:` , puede colocar cualquier dato en el manifiesto. Puede utilizar estos datos en el código de la aplicación para completar las tareas enumeradas anteriormente. Por ejemplo, puede utilizar `skd:{content_id}` para que la aplicación pueda determinar el ID del contenido que se está reproduciendo y solicitar un token para ese contenido específico. También puede, por ejemplo, utilizar `skd:{entitlement_server_url}?cid={content_id}`, de modo que la aplicación no necesite tener codificada la URL del servidor de autorizaciones.

Es posible que no necesite ninguna información en su `skd:` URL si, al iniciarse la reproducción, ya conoce el ID de contenido a través de otros canales. El segundo ejemplo es una solución ideal para probar la configuración, pero también puede utilizarlo en un entorno de producción.

>[!TIP]
>
>Usted determina el formato de `skd:`.

El contenido se obtiene mediante las `skd:` protocolo, pero la solicitud de licencia utiliza `https:`. Las opciones más comunes para hacer frente a estos protocolos son:

* **Prueba inicial de reproducción de extremo a extremo** Al empaquetar el contenido, seleccione una `skd:` URL. Al probar la aplicación, adquiera manualmente una licencia de ExpressPlay y codifique la licencia (un `https:` URL) y URL de contenido en el cargador.

   Por ejemplo:

   ```
   NSString* const PLAYLIST_URL =  
     @"https://{your_content_URL}/{your_manifest}.m3u8"; 
   NSString* const EXPRESSPLAY_TOKEN =  
     @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
       ExpressPlayToken={copy_your_token_to_here}";
   ```

* **La mayoría de los otros casos** Al empaquetar el contenido, seleccione una `skd:` URL que representa de forma exclusiva el ID del contenido. En el cargador, analice `skd:` URL, envíela al servidor para adquirir un token y utilice el token resultante como URL.

   Por ejemplo:

   ```
   - (BOOL)resourceLoader:(AVAssetResourceLoader *)resourceLoader  
         shouldWaitForLoadingOfRequestedResource:(AVAssetResourceLoadingRequest *)loadingRequest { 
       NSURL *url = [[loadingRequest request] URL]; 
       if (![[url scheme] isEqual:@"skd"]) 
           return NO; 
   
       NSString *strUrl = [url absoluteString]; 
       NSLog(@"url is: %@", strUrl); 
   
       strUrl = [strUrl stringByReplacingOccurrencesOfString:@"skd://" withString:@"https://"]; 
   
       NSData *assetId; 
   
       NSData *requestBytes; 
       NSError* error = nil; 
       BOOL handled = NO; 
   
       NSData  *responseData = nil; 
   
       assetId = getMyAssetIdentifierFromURL(url); 
   
       /* Usecase 1: "On Premise Fairplay Server" 
        * Set the strUrl to the OnPremise Fairplay Server Url. The OnPremise Fairplay  
        * Server Url is either hardcoded in the App or derived from strUrl. 
        */ 
   #if 0  
       // Insert your use case 1 codes here: 
       // strUrl = getOnPremiseServerUrl(strUrl, assetId); 
   #endif // 
   
       /* Usecase 2: The strUrl is the entitlement server. 
        * Send assetId to the entitlement server; if the user is allowed to playback  
        * the content, the entitlement server will send back an ExpressPlay Token Url. 
        */ 
   
   #if 0 
       // The hardcoded SEES server: 
       strUrl = @"https://10.0.248.85:8080/sees/SEESServlet"; 
   
       // You can use the following code to simulate a device binding entitlement  
       // request:  
       // First, invoke getExpressPlayTokenUrlFromEntilementServer with  
       // bEnforceDeviceID set to false. When you play the content, the device_id  
       // will be registered on the ExpressPlay Server.  Now change code to set  
       // bEnforceDeviceID to true, and rerun the program. The ExpressPlay token  
       // sent back by the SEES server will be device bound. 
   
       // The strUrl returned below is the ExpressPlay Token URL. 
       strUrl = getExpressPlayTokenUrlFromEntilementServer(strUrl, assetId, true, &error); 
   #endif 
   
       /* Usecase 3: The strUrl is already the ExpressPlay Token Url. 
        */ 
   
       // Read in the certificate 
       NSLog(@"Get Application Certificate"); 
       NSString* certPath = [[NSBundle mainBundle] pathForResource:@"my_certificate.cer"  
                                                            ofType:nil]; 
   
       NSData *appCert = [NSData dataWithContentsOfFile:certPath]; 
   
       // To create the request blob for the server: 
       requestBytes = [loadingRequest streamingContentKeyRequestDataForApp: appCert 
                                                         contentIdentifier:assetId  
                                                                   options:nil  
                                                                     error:&error]; 
       if (requestBytes == nil) { 
           NSLog(@"Error creating server request: %@", error); 
           return false; 
       } 
       // Per the specification, send requestBytes along with the assetId to the Key 
       // Server and obtain the response. 
       NSError *err; 
   
       responseData = getCKCFromExpressPlayService( strUrl, requestBytes, assetId, &err); 
   
       if (responseData != nil) { 
           NSLog(@"Get response data: "); 
           [loadingRequest finishLoadingWithResponse:nil  
                                                data:(NSData *)responseData 
                                            redirect:nil]; 
       } 
       else { 
           [loadingRequest finishLoadingWithError:err]; 
           NSLog(@"bad key response"); 
       } 
       handled = YES; 
   bail: 
       return handled; 
   
   }
   ```

## Habilitar Apple FairPlay en aplicaciones TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Puede implementar Apple FairPlay Streaming, que es la solución DRM de Apple, en sus aplicaciones TVSDK.

1. Cree su cargador de recursos para clientes de FairPlay implementando `PTAVAssetResourceLoaderDelegate`.

   Para obtener más información, consulte [Apple FairPlay en aplicaciones TVSDK](../../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Asegúrese de seguir las instrucciones de la *Guía del programa de transmisión FairPlay* ( *FairPlayStreaming_PG.pdf*), que se incluye en [SDK de FairPlay Server para desarrollar una aplicación compatible con FPS](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   El `resourceLoader:shouldWaitForLoadingOfRequestedResource` es equivalente a lo que hay en `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >En el escenario del servidor de licencias ExpressPlay, para reproducir contenido, cambie el esquema URL en la URL de la solicitud de licencia del servidor ExpressPlay FairPlay desde `skd://` hasta `https://` (o `https://`).

1. Registre el *FairPlay* Cargador de recursos del cliente con `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Si ha escrito su propio servidor de licencias FairPlay o está utilizando un servidor de licencias FairPlay de terceros, consulte al proveedor del servidor de licencias para determinar la URL del servidor de licencias, el formato y cualquier otro requisito.
