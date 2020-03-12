---
description: Puede implementar sus propios resueltores de contenido en función de los resueltores predeterminados.
seo-description: Puede implementar sus propios resueltores de contenido en función de los resueltores predeterminados.
seo-title: Implementar una resolución de contenido personalizada
title: Implementar una resolución de contenido personalizada
uuid: 5f63cc1e-3f4b-460c-9151-2b9d364800e2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Implementar una resolución de contenido personalizada {#implement-a-custom-content-resolver}

Puede implementar sus propios resueltores de contenido en función de los resueltores predeterminados.

Cuando TVSDK genera una nueva oportunidad, se repite a través de los resueltores de contenido registrados que buscan una que sea capaz de resolver esa oportunidad. El primero que vuelve `true` se selecciona para resolver la oportunidad. Si no se puede resolver ningún contenido, se omitirá esa oportunidad. Dado que el proceso de resolución de contenido suele ser asíncrono, la resolución de contenido es responsable de notificar a TVSDK cuando se ha completado el proceso.

1. Implemente su propia personalización `ContentFactory`, ampliando la `ContentFactory` interfaz y anulando `retrieveResolvers`.

   Por ejemplo:

   ```java
   class MyContentFactory extends ContentFactory { 
       @Override 
       public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
           List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
           MediaPlayerItemConfig itemConfig = item.getConfig(); 
           if(itemConfig) { 
               CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
               if (customRanges) { 
                   List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
   
                   if (timeRanges && timeRanges.size() > 0) 
                   { 
                   // CustomRangeResolver is only activated by the presence of CustomRanges in configuration 
                   resolvers.add(new CustomRangeResolver()); 
                   } 
               } 
               AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
               if (metadata) { 
                   if (metadata instanceOf AuditudeSettings)  
                       resolvers.add(new AuditudeResolver(getContext());    
                   } 
               } 
           // add your custom resolver if any 
           resolvers.add(MyOpportunityGenerator(item)); 
           return resolvers; 
       } 
       ... 
   } 
   ```

1. Registre el `ContentFactory` en el `MediaPlayer`.

   Por ejemplo:

   ```java
   //Register the custom content factory with the media player 
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new MyContentFactory()); 
   
   //Pass this config while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config); 
   
   // OR use MediaPlayerItemLoader to pre-load a resource 
   id = 23; 
   itemLoader.load(resource, id, config);
   ```

1. Pase un `AdvertisingMetadata` objeto a TVSDK de la siguiente manera:
   1. Cree un `AdvertisingMetadata` objeto.
   1. Guarde el `AdvertisingMetadata` objeto en `MediaPlayerItemConfig`.

      ```java
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
      
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
      
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      ```

1. Cree una clase de resolución de publicidad personalizada que amplíe la `ContentResolver` clase.
   1. En la resolución de publicidad personalizada, sobrescriba `doConfigure`, `doCanResolve``doResolve`, `doCleanup`:

      ```java
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      Obtendrá su `advertisingMetadata` parte del elemento pasado `doConfigure`:

      ```java
      MediaPlayerItemConfig itemConfig = item.getConfig(); 
      
      AdvertisingMetadata advertisingMetadata =  
        mediaPlayerItemConfig.getAdvertisingMetadata(); 
      ```

   1. Para cada oportunidad de colocación, cree un `List<TimelineOperation>`.

      Este ejemplo `TimelineOperation` proporciona una estructura para `AdBreakPlacement`:

      ```java
      AdBreakPlacement( 
          new AdBreak( ads,    // Vector<Ad> 
                       tracker // Content Tracker 
          ), 
          placementInformation // Retrieved from Opportunity 
      ); 
      ```

   1. Una vez resueltas las publicidades, llame a una de las siguientes funciones:

      * Si la publicidad se resuelve correctamente, llame `process(List<TimelineOperation> proposals)` y `notifyCompleted(Opportunity opportunity)` haga clic en `ContentResolverClient`

         ```java
         _client.process(timelineOperations); 
         _client.notifyCompleted(opportunity); 
         ```

      * Si la resolución de la publicidad falla, llame `notifyResolveError` al `ContentResolverClient`

         ```java
         _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
         ```

         Por ejemplo:

         ```java
         _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
         ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

Esta resolución de publicidad personalizada de ejemplo resuelve una oportunidad y proporciona una publicidad simple:

```java
public class CustomContentResolver extends ContentResolver { 
    protected void doConfigure(MediaPlayerItem item){} 
 
    protected boolean doCanResolve(Opportunity opportunity) {  
        return true;  
    } 
 
    protected void doResolve(Opportunity opportunity) { 
        _client.process(createAdBreakPlacementsFor(opportunity.getPlacement())); 
        _client.notifyCompleted(opportunity); 
    } 
 
    private List<TimelineOperation> createAdBreakPlacementsFor(Placement placementInformation) { 
        List<Ad> ads = new ArrayList<Ad>(); 
        AdAsset adAsset = new AdAsset("101", 15000, new MediaResource( 
          "https: . . ..m3u8", MediaResource.Type.HLS, null), null, null); 
 
        Ad ad = Ad.linearFromAsset("101", adAsset, null, null, false); 
        ads.add(ad); 
        AdBreak adBreak = new AdBreak(ads, null, AdInsertionType.CLIENT_INSERTED); 
 
        List<TimelineOperation> result = new ArrayList<TimelineOperation>(); 
 
        result.add(new AdBreakPlacement(placementInformation, adBreak)); 
        return result; 
    } 
 
    protected void doCleanup() {} 
} 
```

