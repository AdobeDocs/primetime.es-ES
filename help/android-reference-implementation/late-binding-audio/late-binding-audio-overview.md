---
description: Puede habilitar y crear controles para el audio de enlace tardío.
title: Información general
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Información general {#overview}

Puede habilitar y crear controles para el audio de enlace tardío.

El estándar HLS permite flujos multiformato, lo que significa que podemos mantener las pistas de audio y vídeo de un flujo separados entre sí. La pista de vídeo, con varias representaciones (por ejemplo, 240p, 480p, 720p y 1080p) y las pistas de audio (por ejemplo, inglés, español, francés, alemán) se pueden codificar por separado. A continuación, el reproductor de medios elige las pistas de vídeo y audio deseadas y las une sobre la marcha, en el lado del cliente.

Puede implementar varios flujos de trabajo, según la interfaz de usuario del reproductor. El flujo de trabajo general del reproductor Primetime es el siguiente:

1. Cuando el usuario final selecciona un vídeo, se rellena una lista de las pistas de audio disponibles para ese elemento multimedia.
1. Cuando el usuario toca el botón Configuración en la interfaz de usuario, se muestran las opciones de pista de audio.
1. Cuando se selecciona una pista de audio, esta se convierte en la pista de audio activa.
1. El usuario final puede pulsar el botón Configuración para volver a la pista de audio original.

