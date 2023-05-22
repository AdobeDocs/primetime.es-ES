---
description: Puede habilitar y generar controles para enlazar audio en tiempo real.
title: Información general
exl-id: be3b41c5-1c30-430c-9baa-06b6496aceb4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# Información general {#overview}

Puede habilitar y generar controles para enlazar audio en tiempo real.

El estándar HLS permite flujos multiformato, lo que significa que podemos mantener las pistas de audio y vídeo de un flujo separadas entre sí. La pista de vídeo, con varias representaciones (por ejemplo, 240p, 480p, 720p y 1080p) y las pistas de audio (por ejemplo, inglés, español, francés, alemán) se pueden codificar por separado. A continuación, el reproductor de contenidos selecciona las pistas de audio y vídeo que desee y las enlaza sobre la marcha, en el lado del cliente.

Puede implementar varios flujos de trabajo en función de la interfaz de usuario del reproductor. El flujo de trabajo general para el reproductor de Primetime es el siguiente:

1. Cuando el usuario final selecciona un vídeo, se rellena una lista de pistas de audio disponibles para ese elemento de medios.
1. Cuando el usuario pulse el botón Configuración en la interfaz de usuario, se mostrarán las opciones de pista de audio.
1. Cuando se selecciona una pista de audio, esta se convierte en la pista de audio activa.
1. El usuario final puede pulsar el botón Configuración para volver a la pista de audio original.
