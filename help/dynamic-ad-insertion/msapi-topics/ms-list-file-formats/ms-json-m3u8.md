---
description: Si pttrackingmode=simple o ptplayer=ios-mobileweb, el servidor de manifiesto devuelve un archivo con formato JSON que contiene Master-M3U8, una URL que el cliente debe utilizar para solicitar el archivo M3U8 que describe el contenido.
seo-description: Si pttrackingmode=simple o ptplayer=ios-mobileweb, el servidor de manifiesto devuelve un archivo con formato JSON que contiene Master-M3U8, una URL que el cliente debe utilizar para solicitar el archivo M3U8 que describe el contenido.
seo-title: Formato JSON para URL para solicitar lista de reproducción de manifiesto de variante
title: Formato JSON para URL para solicitar lista de reproducción de manifiesto de variante
uuid: 9f9693d0-3c93-4555-b20c-7f4576742f41
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Formato JSON para URL para solicitar lista de reproducción de manifiesto de variante {#json-format-for-url-for-requesting-variant-manifest-playlist}

Si `pttrackingmode=simple` o `ptplayer=ios-mobileweb`, el servidor de manifiesto devuelve un archivo con formato JSON que contiene Master-M3U8, una dirección URL que el cliente debe utilizar para solicitar el archivo M3U8 que describe el contenido.

Es el formato del archivo JSON que contiene la dirección URL `Master-M3U8`.

```
{
"Master-M3U8": "https://manifest.auditude.com/auditude/variant/{publisherAssetID}/
  {sessionId}/{Base 64 of the url of the content}.m3u8
  ?u={Ad Request Id}
  &z={Ad Zone Id}
  &pttrackingmode=simple
  &pttrackingversion=v1
  &{other query parameters}"
}
```
