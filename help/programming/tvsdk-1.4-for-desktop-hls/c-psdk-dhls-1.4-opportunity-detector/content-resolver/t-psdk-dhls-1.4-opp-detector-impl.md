---
description: Puede implementar sus propios detectores de oportunidades.
seo-description: Puede implementar sus propios detectores de oportunidades.
seo-title: Implementar un detector de oportunidades personalizado
title: Implementar un detector de oportunidades personalizado
uuid: 18fb431b-4585-4293-92a7-b77ab7f9b7db
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Implementar un detector de oportunidades personalizado{#implement-a-custom-opportunity-detector}

Puede implementar sus propios detectores de oportunidades.

* Si el generador de oportunidades se basa en `TimedMetadata` objetos asociados con el flujo de medios actual, debe extender el `SpliceOutOpportunityGenerator` valor o `TimedMetadataOpportunityGenerator`.

* Si el generador de oportunidades se basa en datos fuera de banda proporcionados por un servicio externo (como un CIS), entonces debe extender el `OpportunityGenerator`.

1. Cree el generador de oportunidades personalizado.

       Si el generador de oportunidades personalizado se basa en objetos &quot;TimedMetadata&quot;, extienda el parámetro &quot;TimedMetadataOpportunityGenerator&quot; y anule estos métodos:
   
   * `doConfigure` - Este método se llama después de que se haya creado el elemento del reproductor de medios y proporciona al generador de oportunidades la posibilidad de crear un conjunto inicial de oportunidades si es necesario
   * `doProcess` - Este método se llama cada vez que `TimedMetadata` se detecta un nuevo objeto (por ejemplo, para flujos en vivo/lineales cada vez que se actualiza la lista de reproducción/manifiesto)

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

1. Registre la fábrica de contenido personalizado para la reproducción del flujo de medios.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

