---
description: TVSDK le proporciona información para que pueda actuar sobre los anuncios en los que se hace clic. A medida que crea la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en un anuncio en el que se puede hacer clic.
title: Anuncios en los que se puede hacer clic
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Anuncios en los que se puede hacer clic {#clickable-ads}

TVSDK le proporciona información para que pueda actuar sobre los anuncios en los que se hace clic. A medida que crea la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en un anuncio en el que se puede hacer clic.

Para TVSDK para Flash Runtime, solo se puede hacer clic en anuncios lineales.

## Responder a clics en anuncios {#respond-to-clicks-on-ads}

Cuando un usuario hace clic en un anuncio o en un botón relacionado, la aplicación es la encargada de responder. TVSDK proporciona información sobre la dirección URL de destino.

Este ejemplo muestra una forma posible de administrar los clics en publicidad.

1. Cada vez que se reproduce un anuncio, muestre un botón en la parte superior del reproductor de contenidos. Un usuario que hace clic en el anuncio se redirige a la dirección URL del anuncio. Este botón forma parte del [!DNL ClickableAdsOverlay.xml].

   ```xml
      <?xml version="1.0"?> 
   <s:VGroup xmlns:fx="https://ns.adobe.com/mxml/2009"  
       xmlns:s="library://ns.adobe.com/flex/spark" percentWidth="100" horizontalAlign="center">     
           <fx:Declarations><fx:String id="text"/></fx:Declarations> 
           <s:Label text="{text}"  backgroundAlpha="0.75" backgroundColor="#DEDEDE"  
               color="#000000" paddingBottom="5" paddingRight="5" paddingLeft="5"  
               paddingTop="5"/> 
   </s:VGroup>
   ```

1. Incluya esta superposición en la muestra del reproductor de contenidos, [!DNL psdkdemo.xml].

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. Para que la vista solo sea visible cuando se reproduce un anuncio, escuche `onAdStart` y `onAdComplete` eventos distribuidos por .

   ```
   _player.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
   _player.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
   ```

   ```
      private function onAdStarted(event:AdPlaybackEvent):void { 
       var primaryAsset:AdAsset = event.ad.primaryAsset; 
       if (primaryAsset.adClick != null) { 
           clickableAdsOverlay.visible = true;  
       } 
   } 
   private function onAdCompleted(event:AdPlaybackEvent):void { 
       clickableAdsOverlay.visible = false; 
   }
   ```

1. Monitorice las interacciones del usuario con anuncios en los que se puede hacer clic. Cuando el usuario toque o haga clic en el anuncio o el botón, notifique a TVSDK con `notifyClick`.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. Escuche el `AdclickEvent.AD_CLICK` evento.

   Si se está reproduciendo un anuncio, TVSDK envía el `AdClickEvent.AD_CLICK` evento, desde el cual se puede recuperar la URL de pulsación y la información relacionada.

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. Ponga en pausa el reproductor de contenido mientras dirige al usuario a la dirección URL del anuncio.

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. Mostrar la URL de pulsación de publicidad y cualquier información relacionada.

       Por ejemplo, puede mostrarlo de una de las siguientes maneras:
   
   * Abra la URL de pulsación en un explorador de la aplicación.

     En plataformas de escritorio, el área de reproducción de anuncios de vídeo se utiliza generalmente para invocar direcciones URL de pulsación cuando el usuario hace clic.
   * Redirija al usuario al explorador web móvil externo.

     En dispositivos móviles, el área de reproducción de anuncios de vídeo se utiliza para otras funciones, como ocultar y mostrar controles, pausar la reproducción, expandirse a pantalla completa, etc. Por lo tanto, en dispositivos móviles, se suele presentar una vista independiente, como un botón de patrocinador, al usuario como medio para iniciar la URL de pulsación.

1. Cierre la ventana del explorador en la que se muestra la información de pulsaciones y reanude la reproducción del vídeo.
