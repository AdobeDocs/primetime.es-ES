---
description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios que se reproducen localmente.
seo-description: La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios que se reproducen localmente.
seo-title: Reproducción y conmutación por error
title: Reproducción y conmutación por error
uuid: 511f16b9-2b86-42c1-8d89-09b26534200b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Información general {#playback-and-failover-overview}

La transmisión por Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o la reproducción de flujo de un visor significa que la reproducción remota puede no tener la calidad de medios que se reproducen localmente.

>[!IMPORTANT]
>
>Primetime no puede proteger contra fallos como una interrupción de ISP o una desconexión de cable.

El flujo de Primetime proporciona protección de conmutación por error para proteger la reproducción frente a determinados fallos del servidor remoto o fallos operativos, lo que mejora la visualización. A pesar de los problemas de transmisión, TVSDK implementa la protección de conmutación por error para minimizar las interrupciones de reproducción y lograr una reproducción sin problemas. El reproductor de vídeo cambia automáticamente a un conjunto de medios de copia de seguridad cuando no están disponibles representaciones o fragmentos completos.