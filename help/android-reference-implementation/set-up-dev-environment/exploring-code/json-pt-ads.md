---
title: Objeto JSON para anuncios de Primetime
description: El bloque de código siguiente define el objeto JSON de detalles cuando el valor del tipo es Primetime ads.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Objeto JSON para anuncios de Primetime {#json-object-for-primetime-ads}

El bloque de código siguiente define el objeto JSON de detalles cuando el valor del tipo es Primetime ads.

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
| sector | Dominio de anuncios de Primetime que se utiliza para las solicitudes de publicidad. |
| mediaid | El contenido multimedia que se ha configurado en Primetime anuncia para este contenido. |
| zoneid | ID de zona de los anuncios de Primetime. Consulte la documentación de anuncios de Primetime para obtener más información. |
| segmentación | Una matriz de pares de clave/valor que se utiliza para segmentar anuncios específicos del contenido. |

Consulte [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) para obtener más información sobre el valor de estos atributos.
