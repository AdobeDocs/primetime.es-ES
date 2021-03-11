---
description: 'Se han introducido nuevas API que indicarán a TVSDK que ignore el estado de conectividad de red al descargar manifiestos. '
title: Reproducción sin conexión con Android
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# Reproducción sin conexión con Android {#offline-playback-with-android}

Se han introducido las siguientes API que indicarán a TVSDK que ignore el estado de conectividad de red al descargar manifiestos. El estado de conectividad de red se utiliza generalmente durante el flujo de velocidad de bits adaptable (ABR), para determinar si se intenta una alternativa o se espera a que la red se reanude.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

Puede habilitar esta configuración e ignorar la conectividad de red.

Establezca `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` como verdadero. El valor predeterminado de un booleano es false.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
