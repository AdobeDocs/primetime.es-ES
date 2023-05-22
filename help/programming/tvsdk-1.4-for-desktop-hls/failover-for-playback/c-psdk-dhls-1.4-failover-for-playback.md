---
description: El streaming a través de Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o de la reproducción de una transmisión en tiempo real de un usuario significa que la reproducción remota podría no tener la calidad del contenido reproducido localmente.
title: Reproducción y failover
exl-id: 45693d0b-a5fb-4716-a410-ac323950f40b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Información general {#playback-and-failover-overview}

El streaming a través de Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o de la reproducción de una transmisión en tiempo real de un usuario significa que la reproducción remota podría no tener la calidad del contenido reproducido localmente.

Primetime no puede protegerse de errores como una interrupción del ISP o una desconexión del cable. Sin embargo, el streaming de Primetime proporciona protección contra failover para proteger la reproducción de ciertos fallos del servidor remoto o fallos de funcionamiento, lo que mejora la experiencia del usuario. TVSDK implementa la protección contra fallos para minimizar las interrupciones en la reproducción y conseguir una reproducción perfecta a pesar de los problemas de transmisión. El reproductor de vídeo cambia automáticamente a un conjunto de medios de copia de seguridad cuando no están disponibles representaciones o fragmentos completos.
