---
description: Las solicitudes de inserción de anuncios del cliente suelen especificar más de una velocidad de bits en la lista de reproducción con formato M3U8 de la variante. El servidor de manifiesto genera y devuelve un nuevo archivo de variante M3U8 que contiene un vínculo M3U8 independiente para cada velocidad de bits. También genera un ID de grupo único para unir estos M3U8.
seo-description: Las solicitudes de inserción de anuncios del cliente suelen especificar más de una velocidad de bits en la lista de reproducción con formato M3U8 de la variante. El servidor de manifiesto genera y devuelve un nuevo archivo de variante M3U8 que contiene un vínculo M3U8 independiente para cada velocidad de bits. También genera un ID de grupo único para unir estos M3U8.
seo-title: Varios flujos de velocidad de bits
title: Varios flujos de velocidad de bits
uuid: f59cb765-e000-43e0-8d3a-8149a3c5b96e
translation-type: tm+mt
source-git-commit: 2c7ac5c1b2d30b7eb819157ee4568739c1bdfb9d

---


# Varios flujos de velocidad de bits {#multiple-bit-rate-streams}

Las solicitudes de inserción de anuncios del cliente suelen especificar más de una velocidad de bits en la lista de reproducción con formato M3U8 de la variante. El servidor de manifiesto genera y devuelve un nuevo archivo de variante M3U8 que contiene un vínculo M3U8 independiente para cada velocidad de bits. También genera un ID de grupo único para unir estos M3U8.

El servidor de manifiesto utiliza la información de la solicitud de URL de Bootstrap del cliente para recuperar la lista de reproducción de la variante de contenido. Genera una nueva lista de reproducción de variante que contiene vínculos de servidor de manifiesto al contenido de nivel de flujo. El cliente los utiliza para crear solicitudes de inserción de anuncios. Los vínculos de contenido de nivel de flujo del servidor de manifiesto tienen el siguiente formato:

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** El servidor de manifiesto establece este valor en función del tipo de lista de reproducción del contenido: Activo/lineal (#EXT-X-PLAYLIST-TYPE:EVENT) o VOD (#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** ID única del editor para el contenido específico proporcionado en la solicitud de URL de Bootstrap.

* **`rendition`** El servidor de manifiesto lo establece en función del valor BANDWIDTH del flujo de contenido y lo utiliza para coincidir con la velocidad de bits de la publicidad con la velocidad de bits del contenido. La velocidad de bits del anuncio no puede superar la velocidad de bits del contenido a menos que la representación del anuncio con la velocidad de bits más baja lo haga.

* **`groupID`** El servidor de manifiesto genera este valor y lo utiliza para asegurarse de que coloca las publicidades de forma coherente, independientemente de qué representaciones de velocidad de bits solicita las publicidades el cliente.

* **`base64-encoded url of the bit rate stream`** La base64 segura para URL del servidor de manifiesto codifica la dirección URL absoluta del flujo de contenido. Cada flujo tiene su propia dirección URL.

* **`Query parameters`** Parámetros de consulta proporcionados en la solicitud de URL de Bootstrap.

