---
description: TVSDK le proporciona información para que pueda actuar en las publicidades de pulsaciones. A medida que cree la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en una publicidad en la que se pueda hacer clic.
seo-description: TVSDK le proporciona información para que pueda actuar en las publicidades de pulsaciones. A medida que cree la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en una publicidad en la que se pueda hacer clic.
seo-title: Publicidades en las que se puede hacer clic
title: Publicidades en las que se puede hacer clic
uuid: edefbc66-2d30-441d-9c30-256588504463
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Publicidades en las que se puede hacer clic {#clickable-ads}

TVSDK le proporciona información para que pueda actuar en las publicidades de pulsaciones. A medida que cree la interfaz de usuario del reproductor, debe decidir cómo responder cuando un usuario haga clic en una publicidad en la que se pueda hacer clic.

Para TVSDK para Flash Runtime, solo se puede hacer clic en las publicidades lineales.

## Responder a los clics en publicidades {#respond-to-clicks-on-ads}

Cuando un usuario hace clic en una publicidad o en un botón relacionado, la aplicación es responsable de responder. TVSDK proporciona información sobre la dirección URL de destino.

Este ejemplo muestra una forma posible de administrar los clics en publicidad.

1. Cada vez que se reproduce un anuncio, se muestra un botón en la parte superior del reproductor de medios. Un usuario que hace clic en la publicidad se redirige a la dirección URL de la publicidad. Este botón forma parte del [!DNL ClickableAdsOverlay.xml].

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

1. Para hacer que la vista solo esté visible cuando se esté reproduciendo un anuncio, escuche los eventos `onAdStart` y `onAdComplete` enviados por .

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

1. Monitoree las interacciones del usuario en las publicidades en las que se puede hacer clic. Cuando el usuario toque o haga clic en el anuncio o botón, notifique a TVSDK con `notifyClick`.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. Escuche el evento `AdclickEvent.AD_CLICK`.

   Si se está reproduciendo un anuncio, TVSDK distribuye el evento `AdClickEvent.AD_CLICK`, desde el cual puede recuperar la dirección URL de pulsación y la información relacionada.

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. Pause el reproductor multimedia mientras dirige al usuario a la dirección URL de la publicidad.

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. Muestre la dirección URL de pulsaciones de publicidad y cualquier información relacionada.

       Por ejemplo, puede mostrarlo de una de las siguientes maneras:
   
   * Abra la URL de pulsación en un navegador de la aplicación.

      En las plataformas de escritorio, el área de reproducción de anuncios de vídeo generalmente se utiliza para invocar direcciones URL de pulsaciones al hacer clic el usuario.
   * Redirija al usuario al navegador web móvil externo.

      En dispositivos móviles, el área de reproducción de anuncios de vídeo se utiliza para otras funciones, como ocultar y mostrar controles, pausar la reproducción, expandirse a pantalla completa, etc. Por lo tanto, en dispositivos móviles, una vista separada, como un botón de patrocinador, se presenta generalmente al usuario como un medio para iniciar la dirección URL de pulsación.

1. Cierre la ventana del explorador en la que se muestra la información de pulsaciones y reanude la reproducción del vídeo.
