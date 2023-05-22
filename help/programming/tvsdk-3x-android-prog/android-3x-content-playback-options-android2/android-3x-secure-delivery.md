---
description: TVSDK introduce la entrega segura a través de HTTPS.
title: Envío seguro a través de HTTPS
exl-id: 41e2c925-2145-4dfd-909a-aec57dbae9cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# Envío seguro a través de HTTPS {#secure-delivery-https}

Adobe Primetime TVSDK proporciona compatibilidad con el envío HTTPS para todas las llamadas que se originan desde TVSDK, que incluyen

* Llamadas al servidor de Auditude Ad
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
