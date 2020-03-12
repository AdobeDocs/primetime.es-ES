---
description: Puede implementar sus propios resueltores de contenido en función de los resueltores predeterminados.
seo-description: Puede implementar sus propios resueltores de contenido en función de los resueltores predeterminados.
seo-title: Implementar una resolución de contenido personalizada
title: Implementar una resolución de contenido personalizada
uuid: 88627fdc-3b68-4a9f-847e-a490ea8e3034
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementar una resolución de contenido personalizada {#implement-a-custom-content-resolver}

Puede implementar sus propios resueltores de contenido en función de los resueltores predeterminados.

Cuando TVSDK detecta una nueva oportunidad, se repite a través de los resueltores de contenido registrado buscando una que sea capaz de resolver esa oportunidad. El primero que devuelve true se selecciona para resolver la oportunidad. Si no se puede resolver ningún contenido, se omitirá esa oportunidad. Dado que el proceso de resolución de contenido suele ser asincrónico, la resolución de contenido es responsable de notificar cuándo se ha completado el proceso.

1. Cree una `AdvertisingFactory` instancia personalizada y sobrescriba `createContentResolver`.

   Por ejemplo:

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public ContentResolver createContentResolver(MediaPlayerItem item) { 
           Metadata metadata = _mediaPlayer.getCurrentItem().getResource().getMetadata(); 
           if (metadata != null) { 
               if (metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue())) { 
                   return new AuditudeResolver(getActivity().getApplicationContext()); 
               } else if (metadata.containsKey(DefaultMetadataKeys.JSON_METADATA_KEY.getValue())) { 
                   return new MetadataResolver(); 
               } else if (metadata.containsKey(DefaultMetadataKeys.TIME_RANGES_METADATA_KEY.getValue())) { 
                   return new CustomAdMarkersContentResolver(); 
               } else if (metadata.containsKey(CustomAdResolver.CUSTOM_METADATA_KEY)) { 
                   return new CustomAdResolver(); 
               } 
           } 
           return null; 
       } 
       ... 
   }
   ```

1. Registre la fábrica del cliente de publicidad en la `MediaPlayer`.

   Por ejemplo:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Pase un `AdvertisingMetadata` objeto a TVSDK de la siguiente manera:
   1. Cree un `AdvertisingMetadata` objeto y un `MetadataNode` objeto.
   1. Guarde el `AdvertisingMetadata` objeto en `MetadataNode`.

   ```java
   MetadataNode result = new MetadataNode(); 
   result.setNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue(),  
                  advertisingMetadata);
   ```

1. Cree una clase de resolución de publicidad personalizada que amplíe la `ContentResolver` clase.
   1. En la resolución de publicidad personalizada, anule esta función protegida:

      ```java
      void doResolveAds(Metadata metadata,  
                        PlacementOpportunity placementOpportunity)
      ```

      Los metadatos contienen su `AdvertisingMetada`. Utilícelo para la siguiente generación `TimelineOperation` de vectores.

   1. Para cada oportunidad de colocación, cree un `Vector<TimelineOperation>`.

      El vector puede estar vacío, pero no nulo.

      Este ejemplo `TimelineOperation` proporciona una estructura para `AdBreakPlacement`:

      ```java
      AdBreakPlacement(AdBreak.createAdBreak( 
                                ads,       // Vector<Ad> 
                                time,      // Ad Break start time. Note: local time on the timeline 
                                duration,  // Ad Break duration 
                                tag()      // An arbitrary string value that can be attached to  
                                           // the AdBreak object. 
                               ), placementInformation  // Retrieved from PlacementOpportunity 
      )
      ```

   1. Una vez resueltas las publicidades, llame a una de las siguientes funciones:

      * Si la resolución de la publicidad se realiza correctamente: `notifyResolveComplete(Vector<TimelineOperation> proposals)`
      * Si falla la resolución de la publicidad: `notifyResolveError(Error error)`
      Por ejemplo, si falla:

      ```java
      Metadata metadata = new MetadataNode(); 
      metadata.setValue("NATIVE_ERROR_CODE", exception.getCause().toString()); 
      error.setMetadata(metadata);
      ```


<!--<a id="example_4F0D7692A92E480A835D6FDBEDBE75E7"></a>-->

Esta resolución de publicidad personalizada de ejemplo realiza una solicitud HTTP al servidor de publicidad y recibe una respuesta JSON.

```java
public class CustomAdResolver extends ContentResolver { 
    ... 
    @Override 
    protected void doResolveAds(Metadata metadata, PlacementOpportunity placementOpportunity) { 
        ... 
        if (resolveSuccess == true) { 
            notifyResolveComplete(Vector<TimelineOperation> proposals); 
        } 
        else { 
            notifyResolveError(Error error); 
        } 
    } 
    ... 
}
```

Ejemplo de respuesta JSON de servidor de publicidad para un flujo en directo:

```
{     
    "response": { 
        "breaks": [ { 
            "start": 0, 
            "ads": [ { 
                "id": 1001, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/geico/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset1", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } 
        ] }, 
        { 
            "start": -1, 
            "ads": [ { 
                "id": 1003, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/priceline/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset3", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        } ] 
    } 
} 
```

Ejemplo de respuesta JSON de servidor de publicidad para VOD:

```
{     
    "response": { 
        "breaks": [ { 
            "start": 0, 
            "ads": [ { 
                "id": 1001, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/geico/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset1", 
                    "resource_type": "" 
                }, 
                "companion_assets": {  
                } 
            }, 
            { 
                "id": 1002, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/crescent/playlist.m3u8", 
                    "duration": 15000, 
                    "id": "asset2", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        }, 
        { 
            "start": 50000, 
            "ads": [ { 
                "id": 1003, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/priceline/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset3", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        }, 
        { 
            "start": 100000000, 
            "ads": [ { 
                "id": 1004, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/camry/playlist.m3u8", 
                    "duration": 15000, 
                    "id": "asset4", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        } ] 
    } 
} 
```

