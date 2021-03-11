---
description: Para mostrar anuncios de tipo titular, debe crear instancias de banner y permitir que el SDK de TVSDK del explorador escuche eventos relacionados con anuncios.
title: Mostrar anuncios de tipo titular
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Mostrar anuncios de tipo titular {#display-banner-ads}

Para mostrar anuncios de tipo titular, debe crear instancias de banner y permitir que el SDK de TVSDK del explorador escuche eventos relacionados con anuncios.

El TVSDK del explorador proporciona una lista de anuncios de banners complementarios asociados a un anuncio lineal a través del evento `AdobePSDK.PSDKEventType.AD_STARTED` .

Los manifiestos pueden especificar anuncios de banners complementarios mediante:

* Un fragmento HTML
* La dirección URL de una página de iFrame
* La URL de una imagen estática o un archivo SWF de Flash de Adobe

Para cada anuncio complementario, el SDK de explorador indica qué tipos están disponibles para su aplicación.

Agregue un oyente para el evento `AdobePSDK.PSDKEventType.AD_STARTED` que haga lo siguiente:
1. Borra los anuncios existentes en la instancia del banner.
1. Obtiene la lista de anuncios complementarios de `Ad.getCompanionAssets`.
1. Si la lista de anuncios complementarios no está vacía, repita la lista para las instancias de banner.

   Cada instancia de banner (un `AdBannerAsset`) contiene información, como ancho, alto, tipo de recurso (html, iframe o static) y datos necesarios para mostrar el banner complementario.
1. Si una publicidad de vídeo no tiene anuncios complementarios reservados con ella, la lista de recursos complementarios no contiene datos para esa publicidad de vídeo.
1. Envía la información del banner a una función de la página que muestra los banners en una ubicación adecuada.

   Normalmente es `div` y su función utiliza el `div ID` para mostrar el banner. Por ejemplo:

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

