---
title: Objeto JSON para marcadores de anuncios personalizados
description: Objeto JSON para marcadores de anuncios personalizados
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Objeto JSON para marcadores de anuncios personalizados {#json-object-for-custom-ad-markers}

El bloque de código siguiente define el objeto JSON &quot;details&quot; cuando el tipo son marcadores de anuncio personalizados.

El MetadataNode devuelto por IFeedItemAdapter:getStreamMetadata() contiene 2 entradas:
1. una entrada con clave de tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` y valor de una instancia de MetadataNode devuelta por `TimeRangeCollection.toMetadata()`.
1. La segunda entrada tiene una clave de tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` con el valor del atributo *adapt-seek-position* a continuación.

```
“metadata”: {
    “ad” :  {
        “type”: “custom ad markers”,
        “details”: {
            "adjust-seek-position": true,
            "time-ranges": [
                {
                    "begin": 5000,
                    "end":15000
                },
                {
                    "begin": 120000,
                    "end":135000
                }
            ]
        }
    }
}
```

| Propiedad | Descripción |
|---|---|
| ajustar-posición de búsqueda | true o false, se utilizan para establecer el valor de la clave com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED en MetadataNode. |
| intervalos de tiempo | Matriz de objetos JSON que indica el intervalo de tiempo para cada marcador de anuncio. Cada entrada de objeto JSON se asigna a una instancia de com.adobe.mediacore.utils.TimeRange. |
| time-ranges.begin | Valor en ms que indica la hora de inicio del marcador de anuncio. |
| time-ranges.end | Valor en ms que indica la hora de finalización del marcador de anuncio. |

Consulte la documentación de TVSDK para obtener más información sobre cómo funcionan los marcadores de publicidad personalizados.
