---
description: Puede implementar Apple FairPlay Streaming, que es la solución DRM de Apple, en sus aplicaciones TVSDK.
title: Habilitar Apple FairPlay en aplicaciones TVSDK
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Habilitar Apple FairPlay en aplicaciones TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Puede implementar Apple FairPlay Streaming, que es la solución DRM de Apple, en sus aplicaciones TVSDK.

1. Cree su cargador de recursos para clientes de FairPlay implementando `PTAVAssetResourceLoaderDelegate`.

   Para obtener más información, consulte [Apple FairPlay en aplicaciones TVSDK](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

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
