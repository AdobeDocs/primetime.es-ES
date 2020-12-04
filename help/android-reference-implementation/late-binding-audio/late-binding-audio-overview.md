---
description: Puede activar y crear controles para el audio de enlace tardío.
seo-description: Puede activar y crear controles para el audio de enlace tardío.
seo-title: Información general
title: Información general
uuid: 7656f930-f426-426e-bcd4-dfa9d39e7ae4
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Información general {#overview}

Puede activar y crear controles para el audio de enlace tardío.

El estándar HLS permite flujos multiformato, lo que significa que podemos mantener las pistas de audio y vídeo de un flujo separados entre sí. La pista de vídeo, con varias representaciones (por ejemplo, 240p, 480p, 720p y 1080p) y las pistas de audio (por ejemplo, inglés, español, francés, alemán) se pueden codificar por separado. A continuación, el reproductor de medios elige las pistas de audio y vídeo que desee y las enlaza sobre la marcha, en el lado del cliente.

Puede implementar varios flujos de trabajo, según la interfaz de usuario del reproductor. El flujo de trabajo general del reproductor Primetime es el siguiente:

1. Cuando el usuario final selecciona un vídeo, se rellena una lista de pistas de audio disponibles para ese elemento de medios.
1. Cuando el usuario toca el botón Configuración en la interfaz de usuario, se muestran las opciones de la pista de audio.
1. Cuando se selecciona una pista de audio, la pista se convierte en la pista de audio activa.
1. El usuario final puede tocar el botón Configuración para volver a la pista de audio original.

