---
seo-title: Objeto JSON para anuncios Primetime
title: Objeto JSON para anuncios Primetime
uuid: acf968d2-9856-4ed6-a046-1ac17d176571
description: El bloque de código siguiente define los detalles del objeto JSON cuando el valor de tipo es Primetime ads.
seo-description: El bloque de código siguiente define los detalles del objeto JSON cuando el valor de tipo es Primetime ads.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Objeto JSON para publicidades Primetime {#json-object-for-primetime-ads}

El bloque de código siguiente define los detalles del objeto JSON cuando el valor de tipo es Primetime ads.

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
| domain | Dominio de anuncios Primetime que se usará para las solicitudes de publicidad. |
| mediaid | La media configurada en los anuncios Primetime para este contenido. |
| zoneid | Los anuncios de Primetime zoneid. Consulte la documentación de anuncios Primetime para obtener más información. |
| objetivo | Matriz de pares clave/valor que se utiliza para dirigir publicidades específicas para el contenido. |

Consulte [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) para obtener más información sobre el valor de estos atributos.