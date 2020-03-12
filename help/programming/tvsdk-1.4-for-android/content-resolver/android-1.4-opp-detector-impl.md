---
description: Puede implementar sus propios detectores de oportunidades implementando la interfaz PlacementOpportunityDetector.
seo-description: Puede implementar sus propios detectores de oportunidades implementando la interfaz PlacementOpportunityDetector.
seo-title: Implementar un detector de oportunidades personalizado
title: Implementar un detector de oportunidades personalizado
uuid: 012527c5-4ef0-4cd6-a9df-2fb861078a7e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementar un detector de oportunidades personalizado {#implement-a-custom-opportunity-detector}

Puede implementar sus propios detectores de oportunidades implementando la interfaz PlacementOpportunityDetector.

1. Cree una `AdvertisingFactory` instancia personalizada y sobrescriba `createOpportunityDetector`. Por ejemplo:

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

1. Registre la fábrica del cliente de publicidad en la `MediaPlayer`. Por ejemplo:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Cree una clase de detector de oportunidades personalizada que extienda la `PlacementOpportunityDetector` clase.
   1. En el detector de oportunidades personalizado, anule esta función:

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      El `timedMetadataList` contiene la lista de disponibles `TimedMetadata`, que se ordena. Los metadatos contienen los parámetros de objetivo y los parámetros personalizados que se enviarán al proveedor de publicidad.

   1. Para cada `TimedMetadata`, cree un `List<PlacementOpportunity>`. La lista puede estar vacía, pero no ser nula. `PlacementOpportunity` debe tener los atributos siguientes:

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. Después de crear las oportunidades de colocación para todos los objetos de metadatos temporizados detectados, simplemente devuelva la `PlacementOpportunity` lista.

Éste es un detector de oportunidad de colocación personalizado de muestra:

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

