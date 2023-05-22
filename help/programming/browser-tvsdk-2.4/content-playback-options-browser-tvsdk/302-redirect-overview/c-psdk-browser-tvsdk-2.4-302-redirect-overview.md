---
description: La optimización de redireccionamiento 302 minimiza el número de respuestas de redireccionamiento 302, lo que permite que su aplicación equilibre la carga de forma más eficaz.
title: Optimización de redireccionamiento HTTP 302
exl-id: 80d5d38d-c998-4fc0-b527-b38e578d76e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Optimización de redireccionamiento HTTP 302 {#http-redirect-optimization}

La optimización de redireccionamiento 302 minimiza el número de respuestas de redireccionamiento 302, lo que permite que su aplicación equilibre la carga de forma más eficaz.

Si se redirige una solicitud de manifiesto principal y la optimización 302 está habilitada en el reproductor, las solicitudes posteriores realizadas para los recursos de ese manifiesto utilizarán la ubicación de dominio final, lo que evita respuestas 302 adicionales. Esta función está habilitada de forma predeterminada y puede cambiar esta configuración.

>[!IMPORTANT]
>
>Esta función solo es compatible con los exploradores certificados que admiten el `responseURL` propiedad en el `XMLHttpRequest` objeto.

Para la reserva de Flash, recuerde la siguiente información:

* Los usuarios finales deben tener instalado el Flash Player de Adobe versión 23 o posterior.
* Si la integridad del flujo está deshabilitada, la redirección 302 solo se admite en exploradores certificados.

## Desactivación de la optimización de redireccionamiento 302 {#disabling-redirect-optimization}

Puede utilizar la propiedad useRedirectUrl para habilitar el redireccionamiento 302 (true) o deshabilitarlo (false).

Por ejemplo:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
