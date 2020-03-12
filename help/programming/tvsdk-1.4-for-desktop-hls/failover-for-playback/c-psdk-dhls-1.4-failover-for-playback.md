---
description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios reproducidos localmente.
seo-description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios reproducidos localmente.
seo-title: Reproducción y conmutación por error
title: Reproducción y conmutación por error
uuid: 731c087d-9e14-4c7a-a856-c3962b9d7608
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Información general {#playback-and-failover-overview}

La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios reproducidos localmente.

Primetime no puede protegerse de errores como una interrupción de ISP o una desconexión de cable. Sin embargo, el flujo de Primetime proporciona protección de conmutación por error para proteger la reproducción de determinados fallos de servidor remoto o fallos operativos, lo que ofrece una mejor experiencia a los visores. TVSDK implementa la protección de conmutación por error para minimizar las interrupciones de reproducción y lograr una reproducción sin problemas a pesar de los problemas de transmisión. El reproductor de vídeo cambia automáticamente a un conjunto de medios de copia de seguridad cuando no están disponibles representaciones o fragmentos completos.
