---
description: La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a la aplicación equilibrar la carga de manera más eficaz.
seo-description: La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a la aplicación equilibrar la carga de manera más eficaz.
seo-title: Optimización de redireccionamiento HTTP 302
title: Optimización de redireccionamiento HTTP 302
uuid: d3009c6c-320a-4c0f-b6ba-bf6473049823
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Optimización de redireccionamiento HTTP 302 {#http-redirect-optimization}

La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a la aplicación equilibrar la carga de manera más eficaz.

Si se redirige una solicitud de manifiesto principal y se habilita la optimización 302 en el reproductor, las solicitudes posteriores realizadas para los recursos de ese manifiesto utilizarán la ubicación de dominio final, lo que evita las respuestas adicionales 302. Esta función está habilitada de forma predeterminada y puede cambiar esta configuración.

>[!IMPORTANT]
>
>Esta función solo se admite en los exploradores certificados que admiten la `responseURL` propiedad en el `XMLHttpRequest` objeto.

Para Flash fallback, recuerde la siguiente información:

* Los usuarios finales deben tener instalado Adobe Flash Player versión 23 o posterior.
* Si la integridad del flujo está deshabilitada, solo se admite la redirección 302 en exploradores certificados.

## Desactivación de la optimización de redireccionamiento 302 {#disabling-redirect-optimization}

Puede utilizar la propiedad useRedirectUrl para habilitar la redirección 302 (true) o la desactivación (false).

Por ejemplo:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
