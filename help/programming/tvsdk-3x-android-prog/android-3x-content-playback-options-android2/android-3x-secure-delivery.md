---
description: TVSDK introduce la entrega segura a través de HTTPS.
title: Envío seguro a través de HTTPS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# Envío seguro a través de HTTPS {#secure-delivery-https}

Adobe Primetime TVSDK proporciona compatibilidad con el envío HTTPS para todas las llamadas que se originan desde TVSDK, que incluyen

* Llamadas al Auditude y al servidor
* Solicitudes CRS
* Llamadas de licencia DRM
* Pings de Video Analytics
* Pings de facturación

Para utilizar esta función, asegúrese de que los servidores configurados para servir las solicitudes anteriores admitan HTTPS.

Este nuevo comportamiento no está habilitado de forma predeterminada. Utilice lo siguiente para habilitar la entrega segura antes de la llamada a `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
