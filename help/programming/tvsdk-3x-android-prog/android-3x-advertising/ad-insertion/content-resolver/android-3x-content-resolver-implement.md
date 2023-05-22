---
description: Puede implementar sus propias resoluciones de contenido en función de las resoluciones predeterminadas.
title: Implementación de un solucionador de contenido personalizado
exl-id: 1f442e2b-65fc-4040-ada2-7a49e488bdef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Implementación de un solucionador de contenido personalizado {#implement-a-custom-content-resolver}

Puede implementar sus propias resoluciones de contenido en función de las resoluciones predeterminadas.

Cuando TVSDK genera una nueva oportunidad, se repite a través de los solucionadores de contenido registrados que buscan uno que sea capaz de resolver esa oportunidad. El primero que devuelve `true` se selecciona para resolver la oportunidad. Si no hay ningún solucionador de contenido capaz, se omite esa oportunidad. Dado que el proceso de resolución de contenido suele ser asincrónico, el gestor de contenido es responsable de notificar a TVSDK cuando el proceso se haya completado.

1. Implemente su propia aplicación personalizada `ContentFactory`, ampliando el `ContentFactory` interfaz y anulación `retrieveResolvers`.

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

1. Registre el `ContentFactory` a la `MediaPlayer`.

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

1. Pase un `AdvertisingMetadata` para TVSDK como se indica a continuación:
   1. Crear un `AdvertisingMetadata` objeto.
   1. Guarde el `AdvertisingMetadata` objeto a `MediaPlayerItemConfig`.

      ```java
      AdvertisingMetadata advertisingMetadata = new AdvertisingMetadata(); 
      
      advertisingMetadata.setDelayAdLoading(true); 
      ... 
      
      mediaPlayerItemConfig.setAdvertisingMetadata(advertisingMetadata); 
      ```

1. Cree una clase personalizada de resolución de anuncios que extienda el `ContentResolver` clase.
   1. En la resolución de anuncios personalizada, omita `doConfigure`, `doCanResolve`, `doResolve`, `doCleanup`:

      ```java
      void doConfigure(MediaPlayerItem item); 
      boolean doCanResolve(Opportunity opportunity); 
      void doResolve(Opportunity opportunity); 
      void doCleanup();
      ```

      Usted recibe su `advertisingMetadata` del elemento transferido `doConfigure`:

      ```java
      MediaPlayerItemConfig itemConfig = item.getConfig(); 
      
      AdvertisingMetadata advertisingMetadata =  
        mediaPlayerItemConfig.getAdvertisingMetadata(); 
      ```

   1. Para cada oportunidad de ubicación, cree un `List<TimelineOperation>`.

      Esta muestra `TimelineOperation` proporciona una estructura para `AdBreakPlacement`:

      ```java
      AdBreakPlacement( 
          new AdBreak( ads,    // Vector<Ad> 
                       tracker // Content Tracker 
          ), 
          placementInformation // Retrieved from Opportunity 
      ); 
      ```

   1. Una vez resueltos los anuncios, invoque una de las siguientes funciones:

      * Si la resolución del anuncio se realiza correctamente, invoque `process(List<TimelineOperation> proposals)` y `notifyCompleted(Opportunity opportunity)` en el `ContentResolverClient`

         ```java
         _client.process(timelineOperations); 
         _client.notifyCompleted(opportunity); 
         ```

      * Si la resolución del anuncio falla, invoque `notifyResolveError` en el `ContentResolverClient`

         ```java
         _client.notifyFailed(Opportunity opportunity, PSDKErrorCode error);
         ```

         Por ejemplo:

         ```java
         _client.notifyFailed(opportunity, UNSUPPORTED_OPERATION);
         ```

<!--<a id="example_463B718749504A978F0B887786844C39"></a>-->

Este solucionador de anuncios personalizado de muestra resuelve una oportunidad y proporciona un anuncio sencillo:

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
