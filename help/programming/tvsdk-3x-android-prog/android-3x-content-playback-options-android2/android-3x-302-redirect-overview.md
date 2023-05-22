---
description: La optimización de redireccionamiento 302 minimiza el número de respuestas de redireccionamiento 302, lo que permite que su aplicación equilibre la carga de forma más eficaz.
title: Optimización de redireccionamiento HTTP 302
exl-id: a238e90f-3aa1-486b-b57f-d543e4c94b2e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Optimización de redireccionamiento HTTP 302 {#http-redirect-optimization}

La optimización de redireccionamiento 302 minimiza el número de respuestas de redireccionamiento 302, lo que permite que su aplicación equilibre la carga de forma más eficaz.

Si se redirige una solicitud de manifiesto principal y la optimización 302 está habilitada en el reproductor, las solicitudes posteriores realizadas para los recursos de ese manifiesto utilizarán la ubicación de dominio final, lo que evita respuestas 302 adicionales. Esta función está habilitada de forma predeterminada y puede cambiar esta configuración.

## Deshabilitar o habilitar la optimización de redireccionamiento 302 {#section_8977448B268E41D69A8F75B60EB9DA3B}

Utilice el `useRedirectedUrl` propiedad para activar el redireccionamiento 302 ( `true`) o desactivado ( `false`).

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
