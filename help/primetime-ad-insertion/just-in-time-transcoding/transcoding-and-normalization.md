---
title: Transcodificación y normalización
description: Transcodificación y normalización
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
