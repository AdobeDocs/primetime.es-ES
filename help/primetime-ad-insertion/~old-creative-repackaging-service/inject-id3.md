---
description: CRS puede inyectar metadatos temporizados de ID3 en formato HLS y creativos para facilitar el seguimiento de anuncios del lado del cliente.
title: Uso de CRS para insertar etiquetas de metadatos temporizados de ID3
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Uso de CRS para insertar etiquetas de metadatos temporizados de ID3 {#using-crs-to-inject-id-timed-metadata-tags}

CRS puede inyectar metadatos temporizados de ID3 en formato HLS y creativos para facilitar el seguimiento de anuncios del lado del cliente.

El reproductor cliente lee los metadatos ID3 para habilitar el seguimiento de anuncios con precisión de fotogramas.

>[!NOTE]
>
>La inyección de metadatos temporizados ID3 solo funciona en Safari en iOS.

## Flujo de trabajo para CRS para inyección de ID3 {#workflow-for-crs-for-id3-injection}

El flujo de trabajo para la inyección de ID3 es el mismo que en [Detailed Workflows for JIT Repackaging.](../~old-creative-repackaging-service/jit-repackage.md) Si el servidor de manifiesto recibe el  `ptplayer=ios-mobileweb` parámetro, le indica a CRS que inserte paquetes ID3 en el creativo de anuncio transcodificado antes de cargarlo en el servidor CDN.

>[!NOTE]
>
>En una configuración de varias CDN, el servidor de manifiesto utiliza el parámetro `ptcdn` en la URL de arranque para identificar el servidor de CDN para cargar el creativo de publicidad.