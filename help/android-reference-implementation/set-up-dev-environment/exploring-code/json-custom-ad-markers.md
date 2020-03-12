---
seo-title: Objeto JSON para marcadores de publicidad personalizados
title: Objeto JSON para marcadores de publicidad personalizados
uuid: 2c05d9ce-a22f-4829-bfea-9dcf0dc7cd6d
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Objeto JSON para marcadores de publicidad personalizados {#json-object-for-custom-ad-markers}

El bloque de código siguiente define el objeto JSON &quot;details&quot; cuando el tipo es marcadores de publicidad personalizados.

El MetadataNode devuelto por IFeedItemAdapter:getStreamMetadata() contiene 2 entradas:
1. una entrada con clave de tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` y valor de una instancia de MetadataNode devuelta por `TimeRangeCollection.toMetadata()`.
1. La segunda entrada tiene una clave de tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` con el valor del atributo *ajusta-buscar-posición* siguiente.

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
| ajustar-buscar-posición | true o false, se utiliza para establecer el valor de la clave com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED en MetadataNode. |
| intervalos de tiempo | Matriz de objetos JSON que indica el intervalo de tiempo de cada marcador de publicidad. Cada entrada de objeto JSON se asigna a una instancia de com.adobe.mediacore.utils.TimeRange. |
| time-range.begin | Valor en ms que indica la hora de inicio del marcador de publicidad. |
| time-range.end | Valor en ms que indica la hora de finalización del marcador de publicidad. |

Consulte la documentación de TVSDK para obtener más información sobre cómo funcionan los marcadores de publicidad personalizados.
