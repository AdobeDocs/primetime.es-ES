---
description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un espectador significa que la reproducción remota puede no tener la calidad del contenido reproducido localmente.
title: Reproducción y failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# Información general {#playback-and-failover-overview}

La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un espectador significa que la reproducción remota puede no tener la calidad del contenido reproducido localmente.

Primetime no puede protegerse de errores como una interrupción del ISP o una desconexión de cable. Sin embargo, la transmisión de Primetime proporciona protección contra fallos de conmutación por error para proteger la reproducción de ciertos fallos de funcionamiento o fallos de servidor remotos, lo que ofrece una mejor experiencia a los espectadores. TVSDK implementa protección contra fallos para minimizar las interrupciones de reproducción y lograr una reproducción sin problemas a pesar de los problemas de transmisión. El reproductor de vídeo cambia automáticamente a un conjunto de medios de copia de seguridad cuando no hay disponibles representaciones o fragmentos completos.
