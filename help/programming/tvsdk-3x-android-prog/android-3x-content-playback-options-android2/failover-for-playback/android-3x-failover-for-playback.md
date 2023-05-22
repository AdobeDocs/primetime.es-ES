---
description: El streaming a través de Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o de la reproducción de flujo continuo de un espectador significa que la reproducción remota podría no tener la calidad del contenido multimedia que se reproduce localmente.
title: Reproducción y failover
exl-id: ba8326ba-4ff1-46ad-bd18-9c83147ab619
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Información general {#playback-and-failover-overview}

El streaming a través de Internet requiere una conexión constante y estable para reproducir un flujo desde un servidor remoto. Sin embargo, la variabilidad de la conexión a Internet o de la reproducción de flujo continuo de un espectador significa que la reproducción remota podría no tener la calidad del contenido multimedia que se reproduce localmente.

>[!IMPORTANT]
>
>Primetime no puede protegerse de errores como una interrupción del ISP o una desconexión de cable.

El streaming de Primetime proporciona protección contra failover para proteger la reproducción frente a determinados fallos del servidor remoto o fallos de funcionamiento, lo que mejora la experiencia de visualización. A pesar de los problemas de transmisión, TVSDK implementa la protección contra fallos para minimizar las interrupciones de reproducción y lograr una reproducción perfecta. El reproductor de vídeo cambia automáticamente a un conjunto de medios de copia de seguridad cuando no están disponibles representaciones o fragmentos completos.
