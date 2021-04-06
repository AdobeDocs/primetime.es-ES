---
title: Transcodificación y normalización
description: Transcodificación y normalización
copied-description: true
exl-id: 48d9d971-4b15-4f1b-8740-c21983a3e835
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Transcodificación y normalización {#transcoding-and-normalization}

El Ad Insertion de Primetime intentará garantizar una experiencia de visualización coherente en todo el contenido y los anuncios intentando coincidir:

1. Códecs de flujo de origen y tasas de bits, a la vez que se selecciona siempre el elemento creativo de mayor calidad/velocidad de bits al transcodificar

1. Tamaños de fragmento de flujo de origen (HLS/#EXT-X-TARGETDURATION)

1. Formatos creativos preferidos para la transcodificación

1. Nivelación automática de audio para garantizar un nivel dB uniforme en todos los creativos de anuncios.

>[!NOTE]
>
>Los recursos HLS generados por el Ad Insertion Primetime acaba de transcodificarse a tiempo producen activos HLS de la versión 3, independientemente de la versión HLS definida en el contenido.
