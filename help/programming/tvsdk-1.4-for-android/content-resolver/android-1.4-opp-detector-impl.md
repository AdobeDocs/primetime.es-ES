---
description: Puede implementar sus propios detectores de oportunidades implementando la interfaz PlacementOpportunityDetector.
title: Implementación de un detector de oportunidades personalizado
exl-id: d78949a0-2c76-4976-9358-05f3db86781e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Implementación de un detector de oportunidades personalizado {#implement-a-custom-opportunity-detector}

Puede implementar sus propios detectores de oportunidades implementando la interfaz PlacementOpportunityDetector.

1. Crear un personalizado `AdvertisingFactory` instancia y anulación `createOpportunityDetector`. Por ejemplo:

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public PlacementOpportunityDetector createOpportunityDetector(MediaPlayerItem item) { 
           return new CustomPlacementOpportunityDetector(); 
       } 
       ... 
   }
   ```

1. Registre la fábrica del cliente de publicidad en `MediaPlayer`. Por ejemplo:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Cree una clase de detector de oportunidades personalizada que amplíe el `PlacementOpportunityDetector` clase.
   1. En el detector de oportunidades personalizado, anule esta función:

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      El `timedMetadataList` contiene la lista de `TimedMetadata`, que se ordena. Los metadatos contienen los parámetros de objetivo y los parámetros personalizados que se envían al proveedor de publicidad.

   1. Para cada `TimedMetadata`, cree un `List<PlacementOpportunity>`. La lista puede estar vacía, pero no ser nula. `PlacementOpportunity` debe tener los atributos siguientes:

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. Una vez creadas las oportunidades de ubicación para todos los objetos de metadatos cronometrados detectados, simplemente devuelva el `PlacementOpportunity` lista.

Este es un ejemplo de detector de oportunidades de ubicación personalizado:

```java
public class CustomPlacementOpportunityDetector implements PlacementOpportunityDetector { 
    ... 
    @Override 
    public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata) { 
        ... 
        List<PlacementOpportunity> opportunities = new ArrayList<PlacementOpportunity>(); 
 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
 
            if (isOpportunity(timedMetadata)) {        // check if given timedMetadata should be  
                                                       // considered as an opportunity 
 
                // create an object of PlacementOpportunity and add it to the opportunities list 
                PlacementOpportunity opportunity =  
                  createPlacementOpportunity(timedMetadata, airingId, metadata); 
                Opportunities.add(opportunity); 
            } 
        } 
        return opportunities; 
    }    
    ... 
} 
```
