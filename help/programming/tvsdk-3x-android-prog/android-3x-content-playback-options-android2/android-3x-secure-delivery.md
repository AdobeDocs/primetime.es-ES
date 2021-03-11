---
description: TVSDK introduce un envío seguro a través de HTTPS.
title: Envío seguro a través de HTTPS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---


# Envío seguro a través de HTTPS {#secure-delivery-https}

Adobe Primetime TVSDK proporciona compatibilidad con el envío HTTPS para todas las llamadas procedentes de TVSDK, que incluyen

* Llamadas al servidor de Auditude Ad
* Solicitudes CRS
* Llamadas de licencia DRM
* Anuncios de Video Analytics
* Anuncios de facturación

Para utilizar esta función, asegúrese de que los servidores configurados para servir las solicitudes anteriores admitan HTTPS.

Este nuevo comportamiento no está habilitado de forma predeterminada. Utilice lo siguiente para habilitar el envío seguro antes de llamar a `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
