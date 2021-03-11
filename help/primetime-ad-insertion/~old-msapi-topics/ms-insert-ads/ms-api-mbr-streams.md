---
description: Las solicitudes de cliente para inserción de publicidad suelen especificar más de una velocidad de bits en la lista de reproducción con formato M3U8 de la variante. El servidor de manifiestos genera y devuelve un nuevo archivo de variante M3U8 que contiene un vínculo M3U8 independiente para cada velocidad de bits. También genera un ID de grupo único para unir estos M3U8s.
title: Flujos de velocidad de bits múltiples
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Flujos de velocidad de bits múltiples {#multiple-bit-rate-streams}

Las solicitudes de cliente para inserción de publicidad suelen especificar más de una velocidad de bits en la lista de reproducción con formato M3U8 de la variante. El servidor de manifiestos genera y devuelve un nuevo archivo de variante M3U8 que contiene un vínculo M3U8 independiente para cada velocidad de bits. También genera un ID de grupo único para unir estos M3U8s.

El servidor de manifiesto utiliza la información de la solicitud URL del Bootstrap del cliente para recuperar la lista de reproducción de la variante de contenido. Genera una nueva lista de reproducción de variante que contiene vínculos de servidor de manifiesto al contenido de nivel de flujo. El cliente los utiliza para construir solicitudes de inserción de anuncios. Los vínculos de contenido de nivel de flujo del servidor de manifiesto tienen el siguiente formato:

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** El servidor de manifiesto establece este valor en función del tipo de lista de reproducción del contenido: Activo/lineal (#EXT-X-PLAYLIST-TYPE:EVENT) o VOD (#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** ID exclusivo del editor para el contenido específico que se proporciona en la solicitud de URL del Bootstrap.

* **`rendition`** El servidor de manifiesto lo establece en función del valor BANDWIDTH del flujo de contenido y lo utiliza para hacer coincidir la velocidad de bits del anuncio con la velocidad de bits del contenido. La velocidad de bits del anuncio no puede superar la velocidad de bits del contenido a menos que lo haga la representación de anuncio con la tasa de bits más baja.

* **`groupID`** El servidor de manifiesto genera este valor y lo utiliza para asegurarse de que coloca los anuncios de forma consistente, independientemente de las representaciones de velocidad de bits que el cliente solicite.

* **`base64-encoded url of the bit rate stream`** La base64 segura para URL del servidor de manifiesto codifica la dirección URL absoluta del flujo de contenido. Cada flujo tiene su propia dirección URL.

* **`Query parameters`** Parámetros de consulta proporcionados en la solicitud de URL del Bootstrap.

