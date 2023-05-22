---
description: Puede implementar sus propias resoluciones de contenido en función de las resoluciones predeterminadas.
title: Implementación de un solucionador de contenido personalizado
exl-id: abe967a5-ced3-4e23-8671-065e256974d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Implementación de un solucionador de contenido personalizado{#implement-a-custom-content-resolver}

Puede implementar sus propias resoluciones de contenido en función de las resoluciones predeterminadas.

Cuando TVSDK detecta una nueva oportunidad, itera a través de los solucionadores de contenido registrados buscando uno que sea capaz de resolver esa oportunidad utilizando `canResolve` método . El primero que devuelve el valor &quot;True&quot; se selecciona para resolver la oportunidad. Si no hay ningún solucionador de contenido capaz, esa oportunidad se omite. Dado que el proceso de resolución de contenido suele ser asincrónico, el gestor de contenido es responsable de notificar a TVSDK cuando el proceso se haya completado.

* El solucionador de contenido llama a `client.place` para especificar qué operación de cronología debe ejecutar TVSDK (normalmente una ubicación de pausa publicitaria).
* El solucionador de contenido llama a `client.notifyCompleted` si el proceso de resolución se ha realizado correctamente, o `client.notifyFailed` si el proceso falla.

1. Cree una resolución de oportunidades personalizada.

   ```
   public class CustomResolver extends ContentResolver { 
   
       /** 
        * Default constructor. 
        */ 
       public function CustomResolver() { 
       } 
   
       override protected function doConfigure(item:MediaPlayerItem):void { 
           // here you can read any media stream characteristics which 
           // might help configure your content resolver like 
           // - the media player item configuration through the item.config 
           // - the media resource metadata through item.resource.metadata 
       } 
   
       /** 
        * @inheritDoc 
        */ 
       override protected function doCanResolve(opportunity:Opportunity):Boolean { 
           // check if the opportunity can be resolved by this resolver 
           // if yes return true, otherwise return false 
   
           return true; 
       } 
   
       /** 
        * @inheritDoc 
        */ 
       override protected function doResolve(opportunity:Opportunity):void { 
           // start the resolving process 
           // communicate with your custom ad server 
   
           // in this example we assume that: 
           // - if successful, onResolveCompleted method will be invoked 
           // - if failed, onResolveFailed method will be invoked 
       } 
   
       private function onResolveCompleted(response:*):void { 
           try { 
               var proposals:Vector.<TimelineOperation> = new Vector.<TimelineOperation>(); 
   
               // extract the timeline ad placement from the response 
               // and add them to the proposal vector 
               // - extract the ad break 
               // - calculate the placement ( can reuse the opportunity.placement ) 
               // var timelineOperation:AdBreakPlacement = new AdBreakPlacement(placement, adBreak); 
               // proposals.push(timelineOperation); 
   
               client.process(proposals); 
               client.notifyCompleted(_opportunity); 
           } catch (error:Error) { 
               onResolveFailed(error); 
           } 
       } 
   
       private function onResolveFailed(error:Error):void { 
   
           var errorMetadata:Metadata = new Metadata(); 
           MetadataUtils.serializeError(error, errorMetadata); 
   
           var mediaError:MediaError = new MediaError(NotificationCode.CONTENT_RESOLVING_ERROR, errorMetadata); 
           client.notifyFailed(_opportunity, mediaError); 
       } 
   
       ... 
   }
   ```

1. Cree la fábrica de contenido personalizado, que utiliza la resolución de contenido personalizada.

   Por ejemplo:

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
           ... 
   
           /** 
            * @inheritDoc 
            */ 
           override protected function  
             doRetrieveResolvers(item:MediaPlayerItem):Vector.<ContentResolver> { 
               var result:Vector.<ContentResolver> = new Vector.<ContentResolver>(); 
   
               var resource:MediaResource = item.resource; 
   
               if (resource.metadata != null) { 
                   if (resource.metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY)) { 
                       result.push(new AuditudeAdResolver()); 
                   } else if (resource.metadata.containsKey("custom-opportunity-detector")) { 
                       result.push(new CustomResolver()); 
                   } 
               } 
               return result; 
           } 
   }
   ```

1. Registre la fábrica de contenido personalizado para el flujo de medios que se va a reproducir.

   Por ejemplo:

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   var advertisingMetadata:AdvertisingMetadata = new AdvertisingMetadata(); 
   // set any parameter you need for custom ad resolver 
   // advertisingMetadata.setValue("customparam", "customvalue"); 
   
   var metadata:Metadata = new Metadata(); 
   metadata.setMetadata("custom-opportunity-detector", advertisingMetadata); 
   var mediaResource:MediaResource = MediaResource.createFromUrl(url, metadata);
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
