---
title: Objeto JSON para anuncios de Primetime
description: El bloque de código siguiente define el objeto JSON de detalles cuando el valor de tipo son anuncios de Primetime.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Objeto JSON para anuncios de Primetime {#json-object-for-primetime-ads}

El bloque de código siguiente define el objeto JSON de detalles cuando el valor de tipo son anuncios de Primetime.

```
“metadata”: {
    “ad” :  {
        “type”: “Primetime ads”,
        “details”: {
            "domain": "sandbox2.auditude.com",
            "mediaid": "rom_asset_case_1",
            "zoneid": "109754",
            "targeting": [
                {
                    "key": "osmfKeyMulAdsAvail12346",
                    "value": "MulAdsAvail12346"
                }
            ]
        }
    }
}
```

| Propiedad | Descripción |
|---|---|
| domain | Dominio de anuncios de Primetime que se utilizará para las solicitudes de publicidad. |
| mediaid | La mediaid que se ha configurado en los anuncios de Primetime para este contenido. |
| zoneid | El anuncio de Primetime zoneid. Consulte la documentación de anuncios de Primetime para obtener más información. |
| segmentación | Matriz de pares clave/valor que se utiliza para dirigir anuncios específicos para el contenido. |

Consulte [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) para obtener más información sobre el valor de estos atributos.