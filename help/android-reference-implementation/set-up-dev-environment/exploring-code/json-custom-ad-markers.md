---
title: Objeto JSON para marcadores de publicidad personalizados
description: Objeto JSON para marcadores de publicidad personalizados
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Objeto JSON para marcadores de publicidad personalizados {#json-object-for-custom-ad-markers}

El bloque de código siguiente define el objeto JSON de &quot;detalles&quot; cuando el tipo es un marcador de anuncio personalizado.

El MetadataNode devuelto por IFeedItemAdapter:getStreamMetadata() contiene dos entradas:
1. una entrada con clave de tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` y el valor de de una instancia del MetadataNode devuelto por `TimeRangeCollection.toMetadata()`.
1. La segunda entrada tiene una clave de tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` con el valor de *adjust-seek-position* atributo siguiente.

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
| adjust-seek-position | true o false, se utilizan para establecer el valor de la clave com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED en MetadataNode. |
| intervalos de tiempo | Matriz de objetos JSON que indica el intervalo de tiempo para cada marcador de anuncio. Cada entrada de objeto JSON se asigna a una instancia de com.adobe.mediacore.utils.TimeRange. |
| time-ranges.begin | Valor en ms que indica la hora de inicio del marcador de publicidad. |
| time-ranges.end | Valor en ms que indica la hora de finalización del marcador de publicidad. |

Consulte la documentación de TVSDK para obtener más información sobre cómo funcionan los marcadores de publicidad personalizados.
