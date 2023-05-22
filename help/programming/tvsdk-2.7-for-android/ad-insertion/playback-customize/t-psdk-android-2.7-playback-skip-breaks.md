---
description: De forma predeterminada, TVSDK fuerza la reproducción de una pausa publicitaria cuando el usuario realiza una búsqueda sobre una pausa publicitaria. Puede personalizar el comportamiento para omitir una pausa publicitaria si el tiempo transcurrido desde que se completó una pausa anterior se encuentra dentro de un determinado número de minutos.
title: Omitir pausas publicitarias durante un periodo de tiempo
exl-id: 13e34c05-2c43-4459-88ec-5c6cfa8c363d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Omitir pausas publicitarias durante un periodo de tiempo {#skip-ad-breaks-for-a-period-of-time}

De forma predeterminada, TVSDK fuerza la reproducción de una pausa publicitaria cuando el usuario realiza una búsqueda sobre una pausa publicitaria. Puede personalizar el comportamiento para omitir una pausa publicitaria si el tiempo transcurrido desde que se completó una pausa anterior se encuentra dentro de un determinado número de minutos.

>[!IMPORTANT]
>
>Si tiene que completar una búsqueda interna para perdonar un anuncio, puede haber una ligera pausa durante la reproducción.

Para anular el comportamiento predeterminado de pausa publicitaria de TVSDK, puede ampliar el selector predeterminado de políticas publicitarias. Hay cuatro políticas de pausa publicitaria disponibles:

* REPRODUCIR
* OMITIR

   >[!NOTE]
   >
   >Es posible que la política de OMITIR la pausa publicitaria no funcione de la forma esperada en las emisiones en directo cuando un anuncio está presente en el punto activo. Por ejemplo, para un anuncio previo a la emisión, OMITIR provocará una llamada de búsqueda al final de la pausa publicitaria, que podría ser buena que el punto activo. En este caso, TVSDK puede buscar en medio de un anuncio.

* REMOVE_AFTER
* QUITAR

   >[!NOTE]
   >
   >El `REMOVE` la política de pausa publicitaria está prevista para su desaprobación. El Adobe recomienda que utilice la variable `SKIP` política de pausa publicitaria en lugar de `REMOVE`.

El siguiente ejemplo de selector de políticas de publicidad personalizado omite los anuncios en los siguientes cinco minutos (hora del reloj) después de que un usuario haya visto una pausa publicitaria.

1. Cuando el usuario termine de ver una pausa publicitaria, guarde el tiempo actual del sistema.

   ```java
   @Override 
   public void onAdBreakComplete(AdBreak adBreak) { 
       ... 
       if (isShouldPlayUpcomingAdBreakRuleEnabled()) { 
           CustomAdPolicySelector.setLastAdBreakPlayedTime(System.currentTimeMillis()); 
           ... 
       } 
   }
   ```

1. Ampliar `AdPolicySelector`.

   ```java
   package com.adobe.mediacore.sample.advertising; 
   
   import com.adobe.mediacore.MediaPlayerItem; 
   import com.adobe.mediacore.MediaPlayerItemConfig; 
   import com.adobe.mediacore.timeline.advertising.policy.*; 
   import com.adobe.mediacore.timeline.advertising.AdBreakTimelineItem; 
   import com.adobe.mediacore.metadata.AdvertisingMetadata; 
   
   import java.util.ArrayList; 
   import java.util.List; 
   
   public class CustomAdPolicySelector implements AdPolicySelector { 
   
       private static final long MIN_BREAK_INTERVAL = 300000; // 5 minutes for next ad break to be played 
       private MediaPlayerItem _mediaPlayerItem; 
       private static long _lastAdBreakPlayedTime; 
       private AdBreakWatchedPolicy watchedPolicy = AdBreakWatchedPolicy.WATCHED_ON_BEGIN; 
   
       public CustomAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
           _mediaPlayerItem = mediaPlayerItem; 
           _lastAdBreakPlayedTime = 0; 
   
           if (mediaPlayerItem != null) { 
               watchedPolicy = extractWatchedPolicy(mediaPlayerItem.getConfig()); 
           } 
       } 
   
       @Override 
       public AdBreakPolicy selectPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
           if (shouldPlayAdBreaks() && adPolicyInfo.getAdBreakTimelineItems() != null) { 
   
               AdBreakTimelineItem item = adPolicyInfo.getAdBreakTimelineItems().get(0); 
   
               // This condition will remove the pre-roll ad from live stream after watching 
               if (item.getTime() == 0 && _mediaPlayerItem.isLive()) { 
                   return AdBreakPolicy.REMOVE_AFTER_PLAY; 
               } 
               if (item.getTime() == 0) { 
                   return AdBreakPolicy.PLAY; 
               } 
   
               // This condition will remove every ad break that has been watched once.  
               // Comment this section if you want to play watched ad breaks again. 
               if (item.isWatched()) { 
                   return AdBreakPolicy.SKIP; 
               } 
   
               return AdBreakPolicy.REMOVE_AFTER_PLAY; 
           } 
   
           return AdBreakPolicy.SKIP; 
       } 
   
       @Override 
       public List<AdBreakTimelineItem> selectAdBreaksToPlay(AdPolicyInfo adPolicyInfo) { 
   
           if (shouldPlayAdBreaks()) { 
   
               List<AdBreakTimelineItem> timelineItems = adPolicyInfo.getAdBreakTimelineItems(); 
               AdBreakTimelineItem item; 
               List<AdBreakTimelineItem> selectedItems = new ArrayList<AdBreakTimelineItem>(); 
   
               if (timelineItems != null && timelineItems.size() > 0) { 
   
                   // Seek Forward Condition 
                   if (adPolicyInfo.getCurrentTime() <= adPolicyInfo.getSeekToTime()) { 
                       item = timelineItems.get(0); 
   
                       // Resume logic - This will be helpful in resuming the content  
                       // from last saved playback session, and just play the pre-roll ad 
                       if(adPolicyInfo.getCurrentTime() == 0) { 
                           if(item.getTime() == 0 && !item.isWatched()) { 
                               // comment this line if you just need to seek to the user's  
                               // last known position without playing pre-roll ad. ZD#820 
                               selectedItems.add(item); 
                               return selectedItems; 
                           } 
                           else{ 
                               return null; 
                           } 
                       } else { 
                           item = timelineItems.get(timelineItems.size()-1); 
                           if (!item.isWatched()) { 
                               selectedItems.add(item); 
                               return selectedItems; 
                           } 
                       } 
   
                       // Seek backward condition 
                   } else if (adPolicyInfo.getCurrentTime() > adPolicyInfo.getSeekToTime()) { 
                       item = timelineItems.get(0); 
   
                       if(!item.isWatched()) { 
                           selectedItems.add(item); 
                           return selectedItems; 
                       } else { 
                           return null; 
                       } 
                   } 
               } 
           } 
           return null; 
       } 
   
       @Override 
       public AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo) { 
           // Simple Ad Policy selector 
           // if the first ad in the break was watched,  
           // skip to the next add after the seek position 
           // otherwise, play the ads in the break from the beginning 
   
           List<AdBreakTimelineItem> timelineItems = adPolicyInfo.getAdBreakTimelineItems(); 
           if (timelineItems != null && timelineItems.size() > 0) { 
               if (timelineItems.get(0).isWatched()) { 
                   return AdPolicy.SKIP_TO_NEXT_AD_IN_AD_BREAK; 
               } 
           } 
   
           // Resume play from the next ad in the break 
           return AdPolicy.PLAY_FROM_AD_BREAK_BEGIN; 
   
       } 
   
       @Override 
       public AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
           return watchedPolicy; 
       } 
   
       public static void setLastAdBreakPlayedTime(long lastAdBreakPlayedTime) { 
           _lastAdBreakPlayedTime = lastAdBreakPlayedTime; 
       } 
   
       private boolean shouldPlayAdBreaks() { 
           long currentTime = System.currentTimeMillis(); 
   
           if (_lastAdBreakPlayedTime <= 0) { 
               return true; 
           } 
   
           if (_lastAdBreakPlayedTime > 0 &&  
             (currentTime - _lastAdBreakPlayedTime) > MIN_BREAK_INTERVAL) { 
               return true; 
           } 
   
           // return false for not playing Ad if this  
           // Ad occurs with 5 minutes of last Ad playback 
           return false; 
       } 
   
       private AdBreakWatchedPolicy extractWatchedPolicy(MediaPlayerItemConfig config) { 
           if (config != null) { 
               AdvertisingMetadata metadata = config.getAdvertisingMetadata(); 
               if (metadata != null) { 
                   return metadata.getAdBreakWatchedPolicy(); 
               } 
           } 
           return AdBreakWatchedPolicy.WATCHED_ON_BEGIN; 
       } 
   } 
   ```
