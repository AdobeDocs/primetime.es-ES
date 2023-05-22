---
description: CRS puede insertar metadatos cronometrados ID3 en formato HLS y elementos creativos para facilitar el seguimiento de anuncios del lado del cliente.
title: Uso de CRS para insertar etiquetas de metadatos cronometrados con ID3
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Uso de CRS para insertar etiquetas de metadatos cronometrados con ID3 {#using-crs-to-inject-id-timed-metadata-tags}

CRS puede insertar metadatos cronometrados ID3 en formato HLS y elementos creativos para facilitar el seguimiento de anuncios del lado del cliente.

El reproductor cliente lee los metadatos de ID3 para habilitar el seguimiento de anuncios con precisión de fotogramas.

>[!NOTE]
>
>La inyección de metadatos cronometrados con ID3 solo funciona en Safari en iOS.

## Flujo de trabajo para CRS para la inyección de ID3 {#workflow-for-crs-for-id3-injection}

El flujo de trabajo para la inyección de ID3 es el mismo que en [Flujos de trabajo detallados para el reempaquetado JIT.](../~old-creative-repackaging-service/jit-repackage.md) Si el servidor de manifiesto recibe el `ptplayer=ios-mobileweb` , indica a CRS que inserte paquetes de ID3 en el creativo de publicidad transcodificado antes de cargarlo en el servidor CDN.

>[!NOTE]
>
>En una configuración de varias CDN, el servidor de manifiesto utiliza el `ptcdn` en la URL de bootstrap para identificar el servidor CDN en el que se cargará el creativo de publicidad.