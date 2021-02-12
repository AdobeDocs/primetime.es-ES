---
description: La transcodificación Just-in-time puede inyectar metadatos temporizados de ID3 en elementos creativos publicitarios para facilitar el seguimiento de anuncios por parte del cliente.
seo-description: La transcodificación Just-in-time puede inyectar metadatos temporizados de ID3 en formato HLS y creativos para facilitar el seguimiento de anuncios por parte del cliente.
seo-title: Uso de la transcodificación puntual para inyectar etiquetas de metadatos temporizados ID3
title: Uso de la transcodificación puntual para inyectar etiquetas de metadatos temporizados ID3
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Uso de la transcodificación Just-in-Time para inyectar etiquetas de metadatos temporizados de ID3 {#using-crs-to-inject-id-timed-metadata-tags}

CRS puede inyectar metadatos temporizados de ID3 en creativos de publicidad para facilitar el seguimiento de anuncios por parte del cliente.

El reproductor cliente lee los metadatos ID3 para habilitar el seguimiento de anuncios preciso para los marcos.

>[!NOTE]
>
>La inyección de metadatos temporizados ID3 solo funciona para Safari/iOS.

## Flujo de trabajo para CRS para inyección de ID3 {#workflow-for-crs-for-id3-injection}

Si Primetime Ad Insertion recibe el parámetro `ptplayer=ios-mobileweb`, inyectará paquetes ID3 en el elemento creativo de publicidad transcodificado antes de cargar en el CDN de almacenamiento de publicidad adecuado.
