---
description: Para mostrar anuncios en letreros, debe crear instancias de letreros y permitir que el SDK del explorador escuche eventos relacionados con anuncios.
seo-description: Para mostrar anuncios en letreros, debe crear instancias de letreros y permitir que el SDK del explorador escuche eventos relacionados con anuncios.
seo-title: Mostrar publicidades tipo titular
title: Mostrar publicidades tipo titular
uuid: aabc126e-b3aa-42dd-ab50-a7db8e324c50
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Mostrar publicidades tipo titular {#display-banner-ads}

Para mostrar anuncios en letreros, debe crear instancias de letreros y permitir que el SDK del explorador escuche eventos relacionados con anuncios.

El SDK de explorador proporciona una lista de publicidades de titular complementarias que están asociadas con una publicidad lineal a través del `AdobePSDK.PSDKEventType.AD_STARTED` evento.

Los manifiestos pueden especificar publicidades de titular complementarias mediante:

* Un fragmento de código HTML
* Dirección URL de una página de iFrame
* La dirección URL de una imagen estática o un archivo SWF de Adobe Flash

Para cada publicidad complementaria, el SDK del explorador indica qué tipos están disponibles para la aplicación.

Agregue un detector para el evento `AdobePSDK.PSDKEventType.AD_STARTED` que haga lo siguiente:
1. Borra las publicidades existentes en la instancia del letrero.
1. Obtiene la lista de publicidades complementarias de `Ad.getCompanionAssets`.
1. Si la lista de anuncios complementarios no está vacía, repita la lista para las instancias de letrero.

   Cada instancia de pancarta (una `AdBannerAsset`) contiene información, como ancho, alto, tipo de recurso (html, iframe o static) y datos necesarios para mostrar la pancarta adjunta.
1. Si una publicidad de vídeo no tiene anuncios complementarios reservados con ella, la lista de recursos complementarios no contiene datos para esa publicidad de vídeo.
1. Envía la información del letrero a una función de la página que muestra los letreros en una ubicación adecuada.

   Generalmente es un `div`usuario y su función utiliza el `div ID` para mostrar el letrero. Por ejemplo:

   Agregue el detector de eventos:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implementar el controlador de oyentes:

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

   Ejemplo de JavaScript para controlar la visualización:

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

