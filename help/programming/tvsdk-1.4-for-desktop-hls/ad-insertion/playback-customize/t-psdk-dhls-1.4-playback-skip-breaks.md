---
description: De forma predeterminada, TVSDK fuerza la reproducción de una pausa publicitaria cuando el usuario busca durante una pausa publicitaria. Puede personalizar el comportamiento para omitir una pausa publicitaria si el tiempo transcurrido desde la finalización de una pausa anterior es de un número determinado de minutos.
seo-description: De forma predeterminada, TVSDK fuerza la reproducción de una pausa publicitaria cuando el usuario busca durante una pausa publicitaria. Puede personalizar el comportamiento para omitir una pausa publicitaria si el tiempo transcurrido desde la finalización de una pausa anterior es de un número determinado de minutos.
seo-title: Omitir pausas publicitarias durante un período de tiempo
title: Omitir pausas publicitarias durante un período de tiempo
uuid: 1a18d5fd-c957-481b-83ae-2129590c1678
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Omitir pausas publicitarias por un período de tiempo{#skip-ad-breaks-for-a-period-of-time}

De forma predeterminada, TVSDK fuerza la reproducción de una pausa publicitaria cuando el usuario busca durante una pausa publicitaria. Puede personalizar el comportamiento para omitir una pausa publicitaria si el tiempo transcurrido desde la finalización de una pausa anterior es de un número determinado de minutos.

>[!IMPORTANT]
>
>Cuando hay una búsqueda interna para omitir una publicidad, puede que haya una ligera pausa en la reproducción.

El siguiente ejemplo de selector de directivas de publicidad personalizado omite las publicidades en los próximos cinco minutos (tiempo de reloj de pared) después de que un usuario haya visto una pausa publicitaria.

1. Amplíe el selector de directivas de publicidad predeterminado para anular el comportamiento predeterminado.

   ```
   /** 
    * Custom ad policy selector. 
    */ 
   public class CustomAdPolicySelector extends DefaultAdPolicySelector { 
   
       /** 
        * Default constructor. 
        * 
        * @param item Associated media player item. 
        */ 
       public function CustomAdPolicySelector(item:MediaPlayerItem) { 
           super(item); 
   
           item.player.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED,  
                                        onAdBreakCompleted); 
       } 
   
       override public function selectPolicyForAdBreak(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForAdBreak(adPolicyInfo); 
           } 
   
           return AdBreakPolicy.SKIP; 
       } 
   
       override public function selectAdBreaksToPlay(adPolicyInfo:AdPolicyInfo):Vector.<AdBreakTimelineItem> { 
           if (shouldPlayAds()) { 
               return super.selectAdBreaksToPlay(adPolicyInfo); 
           } 
   
           return new Vector.<AdBreakTimelineItem>(); 
       } 
   
       override public function selectPolicyForSeekIntoAd(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForSeekIntoAd(adPolicyInfo); 
           } 
   
           return AdPolicy.SKIP_TO_NEXT_AD_IN_AD_BREAK; 
       } 
   
       private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
           _lastAdBreakPlayedTime = new Date().valueOf(); 
       } 
   
       private function shouldPlayAds():Boolean { 
           var currentTime:Number = new Date().valueOf(); 
           return isNaN(_lastAdBreakPlayedTime) 
                   ||  (currentTime - _lastAdBreakPlayedTime > _minimumInterval); 
       } 
   
       private var _lastAdBreakPlayedTime:Number = NaN; 
       private var _minimumInterval:Number = 300000; // 5 minutes in milliseconds 
   }
   ```

1. Cree una nueva fábrica de publicidad que utilice su selector personalizado.

   ```
   public class CustomAdPolicyContentFactory extends DefaultContentFactory { 
   
       private var _adPolicySelector:CustomAdPolicySelector; 
   
       /** 
        * Default constructor. 
        */ 
       public function CustomAdPolicyContentFactory() { 
   
       } 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
       if (!_adPolicySelector) { 
           _adPolicySelector = new CustomAdPolicySelector(item); 
       } 
   
       return _adPolicySelector; 
       } 
   }
   ```

1. Registre la nueva clase de fábrica de publicidad que se utilizará con MediaPlayer.

   ```
   var mediaResource:MediaResource =  
     MediaResource.createFromUrl("https://example.org/stream.m3u8", null); 
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     PSDKConfig.retrieveMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomAdPolicyContentFactory(); 
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

