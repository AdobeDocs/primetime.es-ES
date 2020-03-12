---
description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios que se reproducen localmente.
seo-description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios que se reproducen localmente.
seo-title: Reproducción y conmutación por error
title: Reproducción y conmutación por error
uuid: 7bbca3fe-88a3-4384-9a63-eb164c956a75
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Información general {#playback-and-failover-overview}

La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios que se reproducen localmente.

>[!IMPORTANT]
>
>Primetime no puede proteger contra fallos como una interrupción de ISP o una desconexión de cable.

El flujo de Primetime proporciona protección de conmutación por error para proteger la reproducción frente a determinados fallos del servidor remoto o fallos operativos, lo que mejora la visualización. A pesar de los problemas de transmisión, TVSDK implementa la protección de conmutación por error para minimizar las interrupciones de reproducción y lograr una reproducción sin problemas. El reproductor de vídeo cambia automáticamente a un conjunto de medios de copia de seguridad cuando no están disponibles representaciones o fragmentos completos.