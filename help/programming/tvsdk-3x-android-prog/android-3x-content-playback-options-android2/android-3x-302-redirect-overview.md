---
description: La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a su aplicación equilibrar la carga de manera más efectiva.
title: Optimización de redireccionamiento HTTP 302
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 2%

---


# Optimización de redireccionamiento HTTP 302 {#http-redirect-optimization}

La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a su aplicación equilibrar la carga de manera más efectiva.

Si se redirige una solicitud de manifiesto principal y se habilita la optimización 302 en el reproductor, las solicitudes posteriores realizadas para los recursos desde ese manifiesto utilizarán la ubicación de dominio final, lo que evita respuestas adicionales 302. Esta función está habilitada de forma predeterminada y puede cambiar esta configuración.

## Deshabilitar o habilitar la optimización de redireccionamiento 302 {#section_8977448B268E41D69A8F75B60EB9DA3B}

Utilice la propiedad `useRedirectedUrl` para activar o desactivar el redireccionamiento 302 ( `true`) ( `false`).

<!--<a id="example_888749F70C8A43279D06A29BD68E7E4D"></a>-->

Por ejemplo:

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration on MediaPlayerItemConfig 
MediaPlayerItemConfig config = new MediaPlayerItemConfig (); 
config.setNetworkConfiguration(networkConfiguration); 
 
//Use this config when loading the MediaPlayerItem or calling replaceCurrentResource
```
