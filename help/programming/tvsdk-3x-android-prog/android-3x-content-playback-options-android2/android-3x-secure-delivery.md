---
description: TVSDK introduce la entrega segura a través de HTTPS.
seo-description: TVSDK introduce la entrega segura a través de HTTPS.
seo-title: Entrega segura a través de HTTPS
title: Entrega segura a través de HTTPS
translation-type: tm+mt
source-git-commit: 4a2271fc481b37bb0a437091de6efe98fcb348d9

---


# Entrega segura a través de HTTPS {#secure-delivery-https}

Adobe Primetime TVSDK ofrece compatibilidad con la entrega HTTPS para todas las llamadas procedentes de TVSDK, que incluyen

* Llamadas al servidor de publicidad Auditude
* Solicitudes de CRS
* Llamadas de licencia DRM
* Analíticos de vídeo ping
* Anuncios de facturación

Para utilizar esta función, asegúrese de que los servidores configurados para atender las solicitudes anteriores admiten HTTPS.

Este nuevo comportamiento no está habilitado de forma predeterminada. Utilice lo siguiente para habilitar la entrega segura antes de llamar a `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
