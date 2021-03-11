---
description: La transcodificación Just-in-time puede insertar metadatos temporizados de ID3 en los creativos de anuncios para facilitar el seguimiento de anuncios del lado del cliente.
title: Uso de la transcodificación justo en el tiempo para insertar etiquetas de metadatos temporizados de ID3
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Uso de la transcodificación Just-in-Time para insertar etiquetas de metadatos temporizados ID3 {#using-crs-to-inject-id-timed-metadata-tags}

CRS puede inyectar metadatos temporizados de ID3 en creativos de anuncios para facilitar el seguimiento de anuncios del lado del cliente.

El reproductor cliente lee los metadatos ID3 para habilitar el seguimiento de anuncios con precisión de fotogramas.

>[!NOTE]
>
>La inyección de metadatos temporizados ID3 solo funciona para Safari/iOS.

## Flujo de trabajo para CRS para inyección de ID3 {#workflow-for-crs-for-id3-injection}

Si el Ad Insertion de Primetime recibe el parámetro `ptplayer=ios-mobileweb`, insertará paquetes ID3 en el creativo de anuncio transcodificado antes de cargarlo en la CDN de almacenamiento de anuncios apropiada.
