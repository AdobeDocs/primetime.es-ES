---
description: Puede implementar sus propios detectores de oportunidad implementando la interfaz PlacementOportunityDetector.
title: Implementar un detector de oportunidades personalizado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---


# Implementar un detector de oportunidades personalizado {#implement-a-custom-opportunity-detector}

Puede implementar sus propios detectores de oportunidad implementando la interfaz PlacementOportunityDetector.

1. Cree una instancia personalizada `AdvertisingFactory` y reemplace `createOpportunityDetector`. Por ejemplo:

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

1. Cree una clase de detector de oportunidades personalizada que amplíe la clase `PlacementOpportunityDetector`.
   1. En el detector de oportunidades personalizado, anule esta función:

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      El `timedMetadataList` contiene la lista de `TimedMetadata` disponibles, que está ordenada. Los metadatos contienen los parámetros de objetivo y los parámetros personalizados que se van a enviar al proveedor de publicidad.

   1. Para cada `TimedMetadata`, cree un `List<PlacementOpportunity>`. La lista puede estar vacía, pero no ser nula. `PlacementOpportunity` debe tener los siguientes atributos:

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. Una vez creadas las oportunidades de colocación para todos los objetos de metadatos temporizados detectados, solo tiene que devolver la lista `PlacementOpportunity`.

Este es un detector de oportunidades de colocación personalizado de ejemplo:

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

