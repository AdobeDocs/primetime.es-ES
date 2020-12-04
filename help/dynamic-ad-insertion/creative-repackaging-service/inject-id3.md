---
description: CRS puede inyectar metadatos temporizados ID3 en formato HLS y creativos para facilitar el seguimiento de anuncios por parte del cliente.
seo-description: CRS puede inyectar metadatos temporizados ID3 en formato HLS y creativos para facilitar el seguimiento de anuncios por parte del cliente.
seo-title: Uso de CRS para insertar etiquetas de metadatos temporizados ID3
title: Uso de CRS para insertar etiquetas de metadatos temporizados ID3
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: c2216a5089d23ca1fcbb77c87b4a01a6fa1807ff
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Uso de CRS para inyectar etiquetas de metadatos temporizados ID3 {#using-crs-to-inject-id-timed-metadata-tags}

CRS puede inyectar metadatos temporizados ID3 en formato HLS y creativos para facilitar el seguimiento de anuncios por parte del cliente.

El reproductor cliente lee los metadatos ID3 para habilitar el seguimiento de anuncios preciso para los marcos.

>[!NOTE]
>
>La inyección de metadatos temporizados ID3 solo funciona en Safari en iOS.

## Flujo de trabajo para CRS para inyección de ID3 {#workflow-for-crs-for-id3-injection}

El flujo de trabajo para la inyección de ID3 es el mismo que en [Flujos de trabajo detallados para el reempaquetado de JIT.](../creative-repackaging-service/jit-repackage.md) Si el servidor de manifiesto recibe el  `ptplayer=ios-mobileweb` parámetro, indica a CRS que inyecte paquetes ID3 en el elemento creativo de anuncio transcodificado antes de cargarlo en el servidor CDN.

>[!NOTE]
>
>En una configuración multiCDN, el servidor de manifiesto utiliza el parámetro `ptcdn` en la URL de inicio para identificar el servidor CDN para cargar el elemento creativo de la publicidad.