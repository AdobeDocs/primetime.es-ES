---
description: 'Se han introducido nuevas API que indicarán a TVSDK que ignore el estado de conectividad de red al descargar manifiestos. '
seo-description: 'Se han introducido nuevas API que indicarán a TVSDK que ignore el estado de conectividad de red al descargar manifiestos. '
seo-title: Reproducción sin conexión con Android
title: Reproducción sin conexión con Android
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Reproducción sin conexión con Android {#offline-playback-with-android}

Se han introducido las siguientes API que indicarán a TVSDK que ignore el estado de conectividad de red al descargar manifiestos. El estado de conectividad de red generalmente se utiliza durante el flujo de velocidad de bits adaptable (ABR) para determinar si se intenta una alternativa o si se espera a que se reanude la red.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

Puede habilitar esta configuración e ignorar la conectividad de red.

Establezca `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` en true. El valor predeterminado de un booleano es false.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
