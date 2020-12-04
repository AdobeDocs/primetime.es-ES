---
description: Puede implementar Apple FairPlay Streaming, que es la solución DRM de Apple, en sus aplicaciones TVSDK.
seo-description: Puede implementar Apple FairPlay Streaming, que es la solución DRM de Apple, en sus aplicaciones TVSDK.
seo-title: Habilitar Apple FairPlay en aplicaciones TVSDK
title: Habilitar Apple FairPlay en aplicaciones TVSDK
uuid: fafffdb9-09f9-45fb-9957-3c6e95ed55f9
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Habilitar Apple FairPlay en aplicaciones TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Puede implementar Apple FairPlay Streaming, que es la solución DRM de Apple, en sus aplicaciones TVSDK.

1. Cree el cargador de recursos del cliente de FairPlay implementando `PTAVAssetResourceLoaderDelegate`.

   Para obtener más información, consulte [Apple FairPlay en aplicaciones TVSDK](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Asegúrese de seguir las instrucciones de la *Guía del Programa de flujo de reproducción equitativa* ( *FairPlayStreaming_PG.pdf*), que se incluye en [FairPlay Server SDK para el desarrollo de una aplicación compatible con FPS](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   El método `resourceLoader:shouldWaitForLoadingOfRequestedResource` es equivalente a lo que se encuentra en `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >En el escenario del servidor de licencias ExpressPlay, para reproducir contenido, cambie el esquema de URL en la URL de solicitud de licencia del servidor ExpressPlay FairPlay de `skd://` a `https://` (o `https://`).

1. Registre el *Cargador de recursos del cliente de FairPlay* con `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Si ha creado su propio servidor de licencias de FairPlay o está utilizando un servidor de licencias de terceros de FairPlay, consulte con el proveedor del servidor de licencias para determinar la URL, el formato y cualquier otro requisito del servidor de licencias.
