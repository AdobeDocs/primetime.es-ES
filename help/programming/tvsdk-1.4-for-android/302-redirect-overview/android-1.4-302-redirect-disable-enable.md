---
description: La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a la aplicación equilibrar la carga de manera más eficaz.
seo-description: La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a la aplicación equilibrar la carga de manera más eficaz.
seo-title: Deshabilitar o habilitar la optimización de redireccionamiento 302
title: Deshabilitar o habilitar la optimización de redireccionamiento 302
uuid: 7561839f-aec6-4a59-a07a-7e4fa043fdc2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Optimización de redireccionamiento HTTP 302 {#http-302-redirect-optimization}

La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a la aplicación equilibrar la carga de manera más eficaz.

Si se redirige una solicitud de manifiesto principal y se habilita la optimización 302 en el reproductor, las solicitudes posteriores realizadas para los recursos de ese manifiesto utilizarán la ubicación de dominio final, lo que evita las respuestas adicionales 302.

Esta función está habilitada de forma predeterminada y puede cambiar esta configuración.

## Deshabilitar o habilitar la optimización de redireccionamiento 302{#disable-or-enable-redirect-optimization}

Utilice la `useRedirectedUrl` propiedad para activar (true) o desactivar (false) la redirección 302.
Por ejemplo:

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration as Metadata: 
MetadataNode resourceMetadata = new MetadataNode();  
resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                         networkConfiguration); 
 
//Call MediaResource.createFromURL to set the metadata: 
MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
  
//Load the resource 
mediaPlayer.replaceCurrentItem(resource);
```

