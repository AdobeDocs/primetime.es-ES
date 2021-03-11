---
description: La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a su aplicación equilibrar la carga de manera más efectiva.
title: Optimización de redireccionamiento HTTP 302
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---


# Optimización de redireccionamiento HTTP 302 {#http-redirect-optimization}

La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a su aplicación equilibrar la carga de manera más efectiva.

Si se redirige una solicitud de manifiesto principal y se habilita la optimización 302 en el reproductor, las solicitudes posteriores realizadas para los recursos desde ese manifiesto utilizarán la ubicación de dominio final, lo que evita respuestas adicionales 302. Esta función está habilitada de forma predeterminada y puede cambiar esta configuración.

>[!IMPORTANT]
>
>Esta función solo se admite en exploradores certificados que admitan la propiedad `responseURL` en el objeto `XMLHttpRequest`.

Para la reserva de Flash, recuerde la siguiente información:

* Los usuarios finales deben tener instalado el Flash Player de Adobe versión 23 o posterior.
* Si se deshabilita la integridad del flujo, solo se admite el redireccionamiento 302 en exploradores certificados.

## Desactivación de la optimización de redireccionamiento 302 {#disabling-redirect-optimization}

Puede utilizar la propiedad useRedirectUrl para habilitar el redireccionamiento 302 (true) o deshabilitar (false).

Por ejemplo:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
