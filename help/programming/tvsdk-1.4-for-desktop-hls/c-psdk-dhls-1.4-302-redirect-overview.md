---
description: La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a su aplicación equilibrar la carga de manera más efectiva.
title: Optimización de redireccionamiento HTTP 302
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---


# Optimización de redireccionamiento HTTP 302{#http-redirect-optimization}

La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a su aplicación equilibrar la carga de manera más efectiva.

Si se redirige una solicitud de manifiesto principal y se habilita la optimización 302 en el reproductor, las solicitudes posteriores realizadas para los recursos desde ese manifiesto utilizarán la ubicación de dominio final, lo que evita respuestas adicionales 302.

Esta función está deshabilitada de forma predeterminada y puede cambiar esta configuración.

Si habilita esta función, solo funciona correctamente si *todas* de las siguientes condiciones son verdaderas; de lo contrario, no se produce optimización de redireccionamiento y continúan produciéndose 302 respuestas:

* La aplicación se ha compilado para el Flash Player de Adobe 11.8, utilizando `-swf-version` 21 o superior.
* Los usuarios finales tienen instalado el Flash Player de Adobe 11.8 o posterior.

>[!IMPORTANT]
>
>Para garantizar que las cookies se pasen con solicitudes de publicidad, deshabilite el redireccionamiento 302. Cuando se habilita el redireccionamiento 302, la solicitud de publicidad puede redirigirse a un dominio diferente del dominio desde el que se originó la cookie.

## Deshabilitar o habilitar la optimización de redireccionamiento 302 {#section_D6687FC44C61446F878008B629A5FA19}

Utilice la propiedad `useRedirectedUrl` para activar o desactivar el redireccionamiento 302 (true) o (false).

<!--<a id="example_B886777252B745AAB48B1FCC42C97A25"></a>-->

Por ejemplo:

```
// Set useRedirectedUrl property to true 
var networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = true; 
  
//Set NetworkConfiguration as Metadata: 
var result:Metadata = new Metadata(); 
result.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                   networkConfiguration); 
  
var mediaResource = new MediaResource( url, MediaResourceType.HLS, result); 
  
// load the resource 
mediaPlayer.replaceCurrentResource( mediaResource, mediaPlayerItemConfig );
```

