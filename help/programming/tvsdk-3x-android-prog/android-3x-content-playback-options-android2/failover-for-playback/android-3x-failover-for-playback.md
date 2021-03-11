---
description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o de la reproducción de flujo de un espectador significa que la reproducción remota puede no tener la calidad del contenido que se reproduce localmente.
title: Reproducción y failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Información general {#playback-and-failover-overview}

La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o de la reproducción de flujo de un espectador significa que la reproducción remota puede no tener la calidad del contenido que se reproduce localmente.

>[!IMPORTANT]
>
>Primetime no puede protegerse de errores como una interrupción del ISP o una desconexión de cable.

La transmisión de Primetime proporciona protección contra failover para proteger la reproducción de ciertos fallos en el servidor remoto o en las operaciones, lo que mejora la experiencia de visualización. A pesar de los problemas de transmisión, TVSDK implementa la protección de conmutación por error para minimizar las interrupciones de reproducción y lograr una reproducción sin problemas. El reproductor de vídeo cambia automáticamente a un conjunto de medios de copia de seguridad cuando no hay disponibles representaciones o fragmentos completos.