---
description: MediaPlayer proporciona una función notifyClick() que envía eventos relacionados con anuncios cuando se reproduce un anuncio en el que se puede hacer clic. Estos eventos proporcionan información sobre las pausas publicitarias y publicitarias que su aplicación puede utilizar para proporcionar funcionalidad de pulsaciones.
title: Gestión de anuncios en los que se puede hacer clic
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Gestionar anuncios en los que se puede hacer clic {#handle-clickable-ads}

MediaPlayer proporciona una función notifyClick() que envía eventos relacionados con anuncios cuando se reproduce un anuncio en el que se puede hacer clic. Estos eventos proporcionan información sobre las pausas publicitarias y publicitarias que su aplicación puede utilizar para proporcionar funcionalidad de pulsaciones.

MediaPlayer desencadena los siguientes eventos cuando se reproduce un anuncio en el que se puede hacer clic:

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

El `AdClickedEvent` contiene la información necesaria para procesar la función de pulsación.

1. Proporcione un control en el reproductor para que los usuarios hagan clic en los anuncios en los que se puede hacer clic.

   Podría ser un botón o cualquier otro elemento para capturar el clic del usuario.
1. Añada un detector de eventos para el evento de clics en publicidad del usuario.

   Por ejemplo:

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. Añada un controlador para el evento de clics del usuario.

   Este controlador debe solicitar a MediaPlayer que active el evento `AdClicked`.

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

1. Agregue oyentes de eventos para el inicio de publicidad de MediaPlayer, haga clic en el anuncio y agregue notificaciones completadas.

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. Agregue controladores de eventos.
a. Gestione el evento de inicio de anuncio.
Esto podría hacer cualquier cosa, como configurar la interfaz de usuario para el usuario.

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

   b. Gestione el evento en el que se ha hecho clic del anuncio.
En este ejemplo, se obtiene información de publicidad del evento y se abre una nueva ventana del explorador con esa información:

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

   c. Gestione el evento de finalización de publicidad.

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
