---
description: La transcodificación Just-In-Time puede insertar metadatos cronometrados de ID3 en los creativos de anuncios para facilitar el seguimiento de anuncios en el lado del cliente.
title: Uso de transcodificación Just-In-Time para insertar etiquetas de metadatos cronometrados ID3
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Uso de transcodificación Just-In-Time para insertar etiquetas de metadatos cronometrados con ID3 {#using-crs-to-inject-id-timed-metadata-tags}

CRS puede insertar metadatos cronometrados ID3 en los creativos de anuncios para facilitar el seguimiento de anuncios del lado del cliente.

El reproductor cliente lee los metadatos de ID3 para habilitar el seguimiento de anuncios con precisión de fotogramas.

>[!NOTE]
>
>Las funciones de inyección de metadatos sincronizadas con ID3 solo para Safari/iOS.

## Flujo de trabajo para CRS para la inyección de ID3 {#workflow-for-crs-for-id3-injection}

Si el Ad Insertion de Primetime recibe el `ptplayer=ios-mobileweb` , insertará paquetes de ID3 en el creativo de publicidad transcodificado antes de cargarlos en la CDN de almacenamiento de publicidad adecuada.
