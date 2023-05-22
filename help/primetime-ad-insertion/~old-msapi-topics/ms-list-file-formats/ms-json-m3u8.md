---
description: Si pttrackingmode=simple o ptplayer=ios-mobileweb, el servidor de manifiesto devuelve un archivo con formato JSON que contiene Master-M3U8, una URL que el cliente debe utilizar para solicitar el archivo M3U8 que describe el contenido.
title: Formato JSON para URL para solicitar la lista de reproducción del manifiesto de variante
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# Formato JSON para URL para solicitar la lista de reproducción del manifiesto de variante {#json-format-for-url-for-requesting-variant-manifest-playlist}

If `pttrackingmode=simple` o `ptplayer=ios-mobileweb`, el servidor de manifiesto devuelve un archivo con formato JSON que contiene Master-M3U8, una URL que el cliente debe utilizar para solicitar el archivo M3U8 que describe el contenido.

Este es el formato del archivo JSON que contiene el `Master-M3U8` URL.

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
