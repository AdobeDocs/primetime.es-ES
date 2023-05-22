---
description: Puede implementar sus propias resoluciones de contenido en función de las resoluciones predeterminadas.
title: Implementación de un solucionador de contenido personalizado
exl-id: 96468f6d-80ad-4721-8ed3-4dbfa2a64b9e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Implementación de un solucionador de contenido personalizado {#implement-a-custom-content-resolver}

Puede implementar sus propias resoluciones de contenido en función de las resoluciones predeterminadas.

Cuando TVSDK detecta una nueva oportunidad, se repite a través de los solucionadores de contenido registrados que buscan uno que sea capaz de resolver esa oportunidad. El primero que devuelve el valor &quot;True&quot; se selecciona para resolver la oportunidad. Si no hay ningún solucionador de contenido capaz, esa oportunidad se omite. Dado que el proceso de resolución de contenido suele ser asincrónico, el solucionador de contenido es responsable de notificar cuando el proceso se haya completado.

1. Crear un personalizado `AdvertisingFactory` instancia y anulación `createContentResolver`.

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

1. Registre la fábrica del cliente de publicidad en `MediaPlayer`.

   Por ejemplo:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Pase un `AdvertisingMetadata` para TVSDK como se indica a continuación:
   1. Crear un `AdvertisingMetadata` objeto y `MetadataNode` objeto.
   1. Guarde el `AdvertisingMetadata` objeto a `MetadataNode`.

   ```java
   MetadataNode result = new MetadataNode(); 
   result.setNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue(),  
                  advertisingMetadata);
   ```

1. Cree una clase personalizada de resolución de anuncios que extienda el `ContentResolver` clase.
   1. En el solucionador de anuncios personalizado, anule esta función protegida:

      ```java
      void doResolveAds(Metadata metadata,  
                        PlacementOpportunity placementOpportunity)
      ```

      Los metadatos contienen su `AdvertisingMetada`. Utilícelo para lo siguiente `TimelineOperation` generación de vectores.

   1. Para cada oportunidad de ubicación, cree un `Vector<TimelineOperation>`.

      El vector puede estar vacío, pero no ser nulo.

      Esta muestra `TimelineOperation` proporciona una estructura para `AdBreakPlacement`:

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

   1. Una vez resueltos los anuncios, invoque una de las siguientes funciones:

      * Si la resolución del anuncio se realiza correctamente: `notifyResolveComplete(Vector<TimelineOperation> proposals)`
      * Si falla la resolución del anuncio: `notifyResolveError(Error error)`

      Por ejemplo, si falla:

      ```java
      Metadata metadata = new MetadataNode(); 
      metadata.setValue("NATIVE_ERROR_CODE", exception.getCause().toString()); 
      error.setMetadata(metadata);
      ```


<!--<a id="example_4F0D7692A92E480A835D6FDBEDBE75E7"></a>-->

Este solucionador de anuncios personalizado de muestra realiza una solicitud HTTP al servidor de publicidad y recibe una respuesta JSON.

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

Ejemplo de respuesta del servidor de publicidad JSON para un flujo en directo:

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

Ejemplo de respuesta del servidor de publicidad JSON para VOD:

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
