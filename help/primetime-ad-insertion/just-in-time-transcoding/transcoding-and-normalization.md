---
title: Transcodificación y normalización
description: null
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# Transcodificación y normalización {#transcoding-and-normalization}

Primetime Ad Insertion intentará garantizar una experiencia de visualización coherente en todo el contenido y los anuncios intentando hacer coincidir:

1. Códecs de flujo de origen y velocidades de bits, a la vez que se selecciona siempre el elemento creativo de mayor calidad/velocidad de bits al transcodificar

1. Tamaños de fragmento de flujo de origen (HLS/#EXT-X-TARGETDURATION)

1. Formatos creativos preferidos para la transcodificación

1. Nivelación automática de audio para garantizar un nivel de dB uniforme en todos los elementos creativos de publicidad.

>[!NOTE]
>
>Los recursos HLS generados por el Ad Insertion Primetime de transcodificación puntual producen recursos HLS de la versión 3, independientemente de qué versión HLS se defina en el contenido.