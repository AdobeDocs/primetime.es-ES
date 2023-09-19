---
description: MediaPlayer proporciona una función notifyClick() que envía eventos relacionados con anuncios cuando se reproduce un anuncio en el que se puede hacer clic. Estos eventos proporcionan información sobre anuncios y pausas publicitarias que la aplicación puede utilizar para ofrecer funciones de pulsación.
title: Gestionar anuncios en los que se puede hacer clic
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Gestionar anuncios en los que se puede hacer clic {#handle-clickable-ads}

MediaPlayer proporciona una función notifyClick() que envía eventos relacionados con anuncios cuando se reproduce un anuncio en el que se puede hacer clic. Estos eventos proporcionan información sobre anuncios y pausas publicitarias que la aplicación puede utilizar para ofrecer funciones de pulsación.

MediaPlayer activa los siguientes eventos cuando se reproduce un anuncio en el que se puede hacer clic:

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

El `AdClickedEvent` contiene la información necesaria para procesar la función de pulsación.

1. Proporcione un control en el reproductor para que los usuarios hagan clic en los anuncios en los que se puede hacer clic.

   Podría ser un botón o cualquier otro elemento para capturar el clic del usuario.
1. Agregue un detector de eventos para el evento de clic en anuncio del usuario.

   Por ejemplo:

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. Agregue un controlador para el evento de clic del usuario.

   Este controlador debe solicitar al MediaPlayer que active el `AdClicked` evento.

   ```
   onAdClick = function (event) { 
       // Get a reference to your player 
       var player = getPlayer(); 
       if (player) { 
           // Call the MediaPlayer's notifyClick function 
           // which gets MediaPlayer to fire AdClicked 
           player.notifyClick(); 
       } 
   } 
   ```

1. Agregue detectores de eventos para el inicio de la publicidad de MediaPlayer, haga clic en el anuncio y añada notificaciones completadas.

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. Agregar controladores de eventos.
a. Controle el evento de inicio del anuncio.
Esto puede hacer cualquier cosa, como configurar la interfaz de usuario para el usuario.

   ```
   onAdStarted = function (event) { 
       if (clickAddButton && event && event.ad) { 
           var adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           if (adClick && adClick.isValid) { 
               // Do some initial processing  
               // when the ad starts, prior 
               // to the user's click. 
           } 
       } 
   }
   ```

   b. Controle el evento de clic en anuncio.
En este ejemplo, obtenemos información de publicidad del evento y abrimos una nueva ventana del explorador con esa información:

   ```
   onAdClickedEvent = function (event) { 
       if (event && event.ad) { 
           var adClick = event.adClick; 
           if (!(adClick && adClick.isValid)) { 
               adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           } 
           if (adClick && adClick.isValid) 
           { 
               // Do something with the currently playing ad 
               window.open(adClick.url); 
           } 
       } 
   }
   ```

   c. Controlar el evento de anuncio completado.

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
