---
title: Transcodificación y normalización
description: Transcodificación y normalización
copied-description: true
exl-id: 48d9d971-4b15-4f1b-8740-c21983a3e835
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Transcodificación y normalización {#transcoding-and-normalization}

El Ad Insertion de Primetime intentará garantizar una experiencia de visualización coherente en todo el contenido y los anuncios intentando hacer coincidir:

1. Códecs de flujo de origen y tasas de bits, al tiempo que siempre se selecciona la creatividad con mayor calidad y velocidad de bits al transcodificar

1. Tamaños de fragmentos de flujo de origen (HLS/#EXT-X-TARGETDURATION)

1. Formatos creativos preferidos para la transcodificación

1. Nivelación automática de audio para garantizar un nivel de dB uniforme en todos los anuncios creativos.

>[!NOTE]
>
>Los recursos HLS generados por el Ad Insertion de Primetime que acaba de transcodificar a tiempo producen recursos HLS de la versión 3, independientemente de la versión HLS definida en el contenido.
