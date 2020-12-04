---
description: Para implementar el flujo de FairPlay en la aplicación TVSDK, debe escribir un cargador de recursos que envíe una solicitud de adquisición de licencia a su servidor de flujo de FairPlay.
seo-description: Para implementar el flujo de FairPlay en la aplicación TVSDK, debe escribir un cargador de recursos que envíe una solicitud de adquisición de licencia a su servidor de flujo de FairPlay.
seo-title: Apple FairPlay en aplicaciones TVSDK
title: Apple FairPlay en aplicaciones TVSDK
uuid: 5796d5af-0018-4c69-a755-65e4819ee838
translation-type: tm+mt
source-git-commit: e1c6ab1d50f9262aaf70aef34854cf293fb4f30d
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# Apple FairPlay en aplicaciones TVSDK {#apple-fairplay-in-tvsdk-applications}

Para implementar el flujo de FairPlay en la aplicación TVSDK, debe escribir un cargador de recursos que envíe una solicitud de adquisición de licencia a su servidor de flujo de FairPlay.

El código del cargador de recursos es responsable de las siguientes tareas:

1. Determine dónde se enviará la solicitud de adquisición de licencia.
1. Dé formato a la solicitud.
1. Proporcione la información necesaria al servidor para que éste pueda decidir si se debe permitir la solicitud.

Por ejemplo, si utiliza el DRM de Primetime Cloud de Adobe con ExpressPlay, el cargador de recursos envía la solicitud a:

```
https://fp-gen.service.expressplay.com
```

El cargador de recursos da formato a la solicitud y adjunta un token de ExpressPlay que autoriza la reproducción a la dirección URL. Al adquirir el token de ExpressPlay, hay varias opciones que considerar. Estas opciones están determinadas por la forma en que se empaqueta el contenido.

Al empaquetar el contenido, el empaquetador inserta `skd:` direcciones URL en el manifiesto M3U8. Después de la entrada `skd:`, puede colocar cualquier dato en el manifiesto. Puede utilizar estos datos en el código de la aplicación para completar las tareas que se enumeran arriba. Por ejemplo, puede utilizar `skd:{content_id}` para que la aplicación pueda determinar el ID del contenido que se está reproduciendo y solicitar un token para ese contenido específico. También puede utilizar, por ejemplo, `skd:{entitlement_server_url}?cid={content_id}` para que la aplicación no necesite tener la URL del servidor de asignación de derechos codificada.

Es posible que no necesite información en la dirección URL `skd:` si, cuando la reproducción inicio, ya conoce el ID de contenido a través de otros canales. El segundo ejemplo es una solución ideal para probar la configuración, pero también puede utilizarla en un entorno de producción.

>[!TIP]
>
>Usted determina el formato de `skd:`.

El contenido se obtiene mediante el protocolo `skd:`, pero la solicitud de licencia utiliza `https:`. Las opciones más comunes para tratar estos protocolos son:

* **Prueba inicial de la** reproducción de extremo a extremoAl empaquetar el contenido, seleccione una  `skd:` URL. Al probar la aplicación, adquiera manualmente una licencia de ExpressPlay y codifique la licencia (una dirección URL `https:`) y la dirección URL de contenido en el cargador.

   Por ejemplo:

   ```
   NSString* const PLAYLIST_URL =  
     @"https://{your_content_URL}/{your_manifest}.m3u8"; 
   NSString* const EXPRESSPLAY_TOKEN =  
     @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
       ExpressPlayToken={copy_your_token_to_here}";
   ```

* **La mayoría de** los demás casosAl empaquetar el contenido, seleccione una  `skd:` dirección URL que represente de forma exclusiva el ID del contenido. En el cargador, analice la dirección URL `skd:`, envíela al servidor para adquirir un token y utilice el token resultante como dirección URL.

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

## Habilitar Apple FairPlay en aplicaciones TVSDK {#section_61CFA3C22FE64F52B2C8CE860B72E88B}

Puede implementar Apple FairPlay Streaming, que es la solución DRM de Apple, en sus aplicaciones TVSDK.

1. Cree el cargador de recursos del cliente de FairPlay implementando `PTAVAssetResourceLoaderDelegate`. Para obtener más información, consulte Apple FairPlay en aplicaciones TVSDK.

   >[!NOTE]
   >
   >Asegúrese de seguir las instrucciones de la *Guía del Programa de flujo de reproducción equitativa* ( *FairPlayStreaming_PG.pdf*), que se incluye en [FairPlay Server SDK para el desarrollo de una aplicación compatible con FPS](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   El método `resourceLoader:shouldWaitForLoadingOfRequestedResource` es equivalente a lo que se encuentra en `AVAssetResourceLoaderDelegate`.

   >[!NOTE]
   >
   >En el escenario del servidor de licencias ExpressPlay, para reproducir contenido, cambie el esquema de URL en la URL de solicitud de licencia del servidor ExpressPlay FairPlay de `skd://` a `https://` (o `https://`).

1. Registre el *Cargador de recursos del cliente de FairPlay* con `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

   >[!NOTE]
   >
   >Si ha creado su propio servidor de licencias de FairPlay o está utilizando un servidor de licencias de terceros de FairPlay, consulte con el proveedor del servidor de licencias para determinar la URL, el formato y cualquier otro requisito del servidor de licencias.