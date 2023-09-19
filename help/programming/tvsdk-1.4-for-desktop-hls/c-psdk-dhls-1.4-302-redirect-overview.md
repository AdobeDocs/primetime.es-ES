---
description: La optimización de redireccionamiento 302 minimiza el número de respuestas de redireccionamiento 302, lo que permite que su aplicación equilibre la carga de forma más eficaz.
title: Optimización de redireccionamiento HTTP 302
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Optimización de redireccionamiento HTTP 302{#http-redirect-optimization}

La optimización de redireccionamiento 302 minimiza el número de respuestas de redireccionamiento 302, lo que permite que su aplicación equilibre la carga de forma más eficaz.

Si se redirige una solicitud de manifiesto principal y la optimización 302 está habilitada en el reproductor, las solicitudes posteriores realizadas para los recursos de ese manifiesto utilizarán la ubicación de dominio final, lo que evita respuestas 302 adicionales.

Esta función está deshabilitada de forma predeterminada y puede cambiar esta configuración.

Si activa esta función, solo funcionará correctamente si *todo* de las siguientes condiciones son verdaderas; de lo contrario, no se produce ninguna optimización de redireccionamiento y siguen produciéndose respuestas 302:

* Su aplicación se compiló para el Flash Player de Adobe 11.8, usando `-swf-version` 21 o superior.
* Los usuarios finales tienen instalado el Flash Player de Adobe 11.8 o posterior.

>[!IMPORTANT]
>
>Para asegurarse de que las cookies se pasan con solicitudes de publicidad, deshabilite el redireccionamiento 302. Cuando la redirección 302 está habilitada, la solicitud de publicidad puede redirigirse a un dominio diferente del dominio desde el que se originó la cookie.

## Deshabilitar o habilitar la optimización de redireccionamiento 302 {#section_D6687FC44C61446F878008B629A5FA19}

Utilice el `useRedirectedUrl` para activar (true) o desactivar (false) el redireccionamiento 302.

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
