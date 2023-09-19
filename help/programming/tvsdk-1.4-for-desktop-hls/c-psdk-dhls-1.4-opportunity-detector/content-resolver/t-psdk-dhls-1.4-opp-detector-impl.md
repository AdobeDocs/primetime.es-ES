---
description: Puede implementar sus propios detectores de oportunidades.
title: Implementación de un detector de oportunidades personalizado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# Implementación de un detector de oportunidades personalizado{#implement-a-custom-opportunity-detector}

Puede implementar sus propios detectores de oportunidades.

* Si el generador de oportunidades se basa en `TimedMetadata` objetos asociados con el flujo de medios actual, debe ampliar el `SpliceOutOpportunityGenerator` o `TimedMetadataOpportunityGenerator`.

* Si el generador de oportunidades se basa en datos fuera de banda proporcionados por un servicio externo (como un CIS), debe ampliar el `OpportunityGenerator`.

1. Cree el generador de oportunidades personalizado.

       Si el generador de oportunidades personalizado se basa en objetos TimedMetadata, amplíe TimedMetadataOpportunityGenerator y anule estos métodos:
   
   * `doConfigure` : se llama a este método después de crear el elemento del reproductor de contenidos, y proporciona al generador de oportunidades la posibilidad de crear un conjunto inicial de oportunidades si es necesario
   * `doProcess` - Se llama a este método cada vez que se crea un nuevo `TimedMetadata` se detecta (por ejemplo, para emisiones en directo/lineales cada vez que se actualiza la lista de reproducción/manifiesto)

   ```
   public class CustomOpportunityGenerator extends TimedMetadataOpportunityGenerator { 
       override protected function doConfigure(playhead:Number, playbackRange:TimeRange):void { 
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
   
           // the item property indicates the current MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadataCollection:Vector.<TimedMetadata> = item.timedMetadata; 
       } 
   
       override protected function doProcess(timedMetadata:TimedMetadata):void { 
           ... 
   
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve(opportunity); 
       }  
       ... 
   }
   ```

1. Cree la fábrica de contenido personalizado, que utiliza el generador de oportunidades personalizado.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       ... 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
           var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
           result.push(new CustomOpportunityGenerator()); 
   
           return result; 
       } 
   }
   ```

1. Registre la fábrica de contenido personalizado para el flujo de medios que se va a reproducir.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
