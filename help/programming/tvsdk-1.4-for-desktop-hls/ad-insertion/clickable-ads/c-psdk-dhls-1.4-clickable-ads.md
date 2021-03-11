---
description: TVSDK le proporciona información para que pueda actuar sobre los anuncios pulsados. A medida que crea la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario hace clic en un anuncio en el que se puede hacer clic.
title: Anuncios en los que se puede hacer clic
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Anuncios en los que se puede hacer clic {#clickable-ads}

TVSDK le proporciona información para que pueda actuar sobre los anuncios pulsados. A medida que crea la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario hace clic en un anuncio en el que se puede hacer clic.

Para TVSDK para el tiempo de ejecución de Flash, solo se puede hacer clic en los anuncios lineales.

## Responder a clics en anuncios {#respond-to-clicks-on-ads}

Cuando un usuario hace clic en un anuncio o en un botón relacionado, la aplicación es responsable de responder. TVSDK proporciona información sobre la dirección URL de destino.

Este ejemplo muestra una forma posible de administrar los clics en publicidad.

1. Cada vez que se reproduce un anuncio, muestra un botón sobre el reproductor de contenidos. Un usuario que hace clic en la publicidad se redirige a la dirección URL de la publicidad. Este botón forma parte del [!DNL ClickableAdsOverlay.xml].

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

1. Incluya esta superposición en nuestro ejemplo de reproductor de medios, [!DNL psdkdemo.xml].

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. Para que la vista solo esté visible cuando se está reproduciendo un anuncio, escuche los eventos `onAdStart` y `onAdComplete` distribuidos por .

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

1. Monitorice las interacciones del usuario en los anuncios en los que se puede hacer clic. Cuando el usuario toque o haga clic en el anuncio o botón, notifique a TVSDK con `notifyClick`.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. Escuche el evento `AdclickEvent.AD_CLICK`.

   Si se está reproduciendo un anuncio, TVSDK distribuye el evento `AdClickEvent.AD_CLICK` desde el cual puede recuperar la dirección URL de pulsación y la información relacionada.

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. Pause el reproductor de contenidos mientras dirige al usuario a la dirección URL de la publicidad.

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. Muestre la dirección URL de pulsación de publicidad y cualquier información relacionada.

       Por ejemplo, puede mostrarlo de una de las siguientes maneras:
   
   * Abra la URL de pulsación en un explorador dentro de la aplicación.

      En las plataformas de escritorio, el área de reproducción de anuncios de vídeo se utiliza generalmente para invocar direcciones URL de pulsaciones al hacer clic en el usuario.
   * Redirija al usuario al explorador web móvil externo.

      En dispositivos móviles, el área de reproducción de anuncios de vídeo se utiliza para otras funciones, como ocultar y mostrar controles, pausar la reproducción, expandirse a pantalla completa, etc. Por lo tanto, en los dispositivos móviles, normalmente se presenta al usuario una vista independiente, como un botón de patrocinador, como un medio para iniciar la URL de pulsación.

1. Cierre la ventana del explorador en la que se muestra la información de pulsaciones y reanude la reproducción del vídeo.
