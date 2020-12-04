---
description: La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a la aplicación equilibrar la carga de manera más eficaz.
seo-description: La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a la aplicación equilibrar la carga de manera más eficaz.
seo-title: Optimización de redireccionamiento HTTP 302
title: Optimización de redireccionamiento HTTP 302
uuid: 58593d5f-a639-4d87-9589-dba6b2dbba38
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Optimización de redireccionamiento HTTP 302{#http-redirect-optimization}

La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a la aplicación equilibrar la carga de manera más eficaz.

Si se redirige una solicitud de manifiesto principal y se habilita la optimización 302 en el reproductor, las solicitudes posteriores realizadas para los recursos de ese manifiesto utilizarán la ubicación de dominio final, lo que evita las respuestas adicionales 302.

Esta función está deshabilitada de forma predeterminada y puede cambiar esta configuración.

Si habilita esta función, sólo funciona correctamente si *todas* de las siguientes condiciones son verdaderas; de lo contrario, no se produce ninguna optimización de redireccionamiento y continúan produciéndose 302 respuestas:

* La aplicación se compiló para Adobe Flash Player 11.8, con `-swf-version` 21 o superior.
* Los usuarios finales tienen instalado Adobe Flash Player 11.8 o posterior.

>[!IMPORTANT]
>
>Para asegurarse de que las cookies se pasan con solicitudes de publicidad, deshabilite la redirección 302. Cuando se habilita la redirección 302, la solicitud de publicidad puede redirigirse a un dominio diferente del dominio desde el que se originó la cookie.

## Deshabilitar o habilitar la optimización de redireccionamiento 302 {#section_D6687FC44C61446F878008B629A5FA19}

Utilice la propiedad `useRedirectedUrl` para activar (true) o desactivar (false) la redirección 302.

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

