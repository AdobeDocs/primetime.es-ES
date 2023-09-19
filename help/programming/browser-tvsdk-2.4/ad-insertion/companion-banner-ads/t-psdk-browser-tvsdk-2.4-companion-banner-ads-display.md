---
description: Para mostrar anuncios de banner, debe crear instancias de banner y permitir que el TVSDK del explorador detecte eventos relacionados con el anuncio.
title: Mostrar anuncios de banner
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Mostrar anuncios de banner {#display-banner-ads}

Para mostrar anuncios de banner, debe crear instancias de banner y permitir que el TVSDK del explorador detecte eventos relacionados con el anuncio.

TVSDK del explorador proporciona una lista de anuncios de banner complementarios asociados a un anuncio lineal a través del `AdobePSDK.PSDKEventType.AD_STARTED` evento.

Los manifiestos pueden especificar anuncios de banner complementarios mediante:

* Un fragmento de HTML
* La dirección URL de una página iFrame
* La URL de una imagen estática o un archivo del SWF del Flash de Adobe

Para cada anuncio complementario, TVSDK del explorador indica qué tipos están disponibles para su aplicación.

Agregar un oyente para el evento `AdobePSDK.PSDKEventType.AD_STARTED` que hace lo siguiente:
1. Borra los anuncios existentes en la instancia de banner.
1. Obtiene la lista de anuncios complementarios de `Ad.getCompanionAssets`.
1. Si la lista de anuncios complementarios no está vacía, itere en la lista de instancias de banner.

   Cada instancia de banner (un `AdBannerAsset`) contiene información, como anchura, altura, tipo de recurso (html, iframe o estático) y datos necesarios para mostrar el banner complementario.
1. Si un anuncio de vídeo no tiene anuncios complementarios reservados con él, la lista de recursos complementarios no contiene datos para ese anuncio de vídeo.
1. Envía la información del titular a una función de la página que muestra los titulares en una ubicación adecuada.

   Esto suele ser un `div`, y la función utiliza el `div ID` para mostrar el titular. Por ejemplo:

   Añada el detector de eventos:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implemente el controlador de escucha:

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void 
   { 
       // check if there are any companion banner 
       if (event.ad && event.ad.companionAssets  
                    && event.ad.companionAssets.length > 0) { 
            for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
               if (ExternalInterface.available) { 
                   //-- call the java script that will handle the banner display. 
                   ExternalInterface.call('addBanner', banner.resourceType,  
                       banner.width, banner.height, banner.bannerData); 
                } 
            } 
        }  
        //...        
   }
   ```

   Ejemplo de JavaScript para gestionar la visualización:

   ```js
   function displayCompanion (resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
       var bannerDiv = document.getElementById('banner' + width + 'x' + height);  
   
       // Assuming that there is an HTML element on the page  
       // with an id of "banner300x250", for example 
       if (bannerDiv !== null) { 
           bannerDiv.innerHTML = data; 
       } 
   }
   ```
