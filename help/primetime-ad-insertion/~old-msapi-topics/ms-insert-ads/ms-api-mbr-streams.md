---
description: Las solicitudes de los clientes para la inserción de anuncios suelen especificar más de una velocidad de bits en la lista de reproducción con formato M3U8 de la variante. El servidor de manifiesto genera y devuelve un nuevo archivo de variante M3U8 que contiene un vínculo M3U8 independiente para cada velocidad de bits. También genera un ID de grupo único para unir estos M3U8.
title: Varias secuencias de velocidad de bits
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Varias secuencias de velocidad de bits {#multiple-bit-rate-streams}

Las solicitudes de los clientes para la inserción de anuncios suelen especificar más de una velocidad de bits en la lista de reproducción con formato M3U8 de la variante. El servidor de manifiesto genera y devuelve un nuevo archivo de variante M3U8 que contiene un vínculo M3U8 independiente para cada velocidad de bits. También genera un ID de grupo único para unir estos M3U8.

El servidor de manifiesto utiliza la información de la solicitud de URL del Bootstrap del cliente para recuperar la lista de reproducción de la variante de contenido. Genera una nueva lista de reproducción de variante que contiene vínculos de servidor de manifiesto al contenido de nivel de flujo. El cliente los utiliza para construir solicitudes de inserción de publicidad. Los vínculos de contenido de nivel de flujo del servidor de manifiesto tienen el siguiente formato:

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** El servidor de manifiesto establece este valor en función del tipo de lista de reproducción del contenido: Live/linear (#EXT-X-PLAYLIST-TYPE:EVENT) o VOD (#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** ID único del publicador para el contenido específico proporcionado en la solicitud de URL del Bootstrap.

* **`rendition`** El servidor de manifiesto lo establece en función del valor BANDWIDTH del flujo de contenido y lo utiliza para hacer coincidir la velocidad de bits del anuncio con la velocidad de bits del contenido. La velocidad de bits del anuncio no puede superar la velocidad de bits del contenido a menos que lo haga la representación del anuncio con la velocidad de bits más baja.

* **`groupID`** El servidor de manifiestos genera este valor y lo utiliza para asegurarse de que coloca anuncios de forma coherente, independientemente de las representaciones de velocidad de bits para las que el cliente solicite los anuncios.

* **`base64-encoded url of the bit rate stream`** El servidor de manifiesto URL-safe base64 codifica la URL absoluta de la secuencia de contenido. Cada flujo tiene su propia URL.

* **`Query parameters`** Parámetros de consulta proporcionados en la solicitud de URL del Bootstrap.

