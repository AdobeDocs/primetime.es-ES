---
description: Se han introducido nuevas API que indicarán a TVSDK que ignore el estado de conectividad de red al descargar manifiestos.
title: Reproducción sin conexión con Android
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Reproducción sin conexión con Android {#offline-playback-with-android}

Se han introducido las siguientes API que indicarán a TVSDK que ignore el estado de conectividad de red al descargar manifiestos. El estado de conectividad de red se utiliza generalmente durante la transmisión de velocidad de bits adaptable (ABR), para determinar si se intenta una reserva o se espera a que se reanude la red.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

Puede habilitar esta configuración e ignorar la conectividad de red.

Establecer `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` a true. El valor predeterminado de un booleano es false.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
