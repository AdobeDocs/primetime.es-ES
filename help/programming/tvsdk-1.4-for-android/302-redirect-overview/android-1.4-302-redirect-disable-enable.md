---
description: La optimización de redireccionamiento 302 minimiza el número de respuestas de redireccionamiento 302, lo que permite que su aplicación equilibre la carga de forma más eficaz.
title: Deshabilitar o habilitar la optimización de redireccionamiento 302
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# Optimización de redireccionamiento HTTP 302 {#http-302-redirect-optimization}

La optimización de redireccionamiento 302 minimiza el número de respuestas de redireccionamiento 302, lo que permite que su aplicación equilibre la carga de forma más eficaz.

Si se redirige una solicitud de manifiesto principal y la optimización 302 está habilitada en el reproductor, las solicitudes posteriores realizadas para los recursos de ese manifiesto utilizarán la ubicación de dominio final, lo que evita respuestas 302 adicionales.

Esta función está habilitada de forma predeterminada y puede cambiar esta configuración.

## Deshabilitar o habilitar la optimización de redireccionamiento 302{#disable-or-enable-redirect-optimization}

Utilice el `useRedirectedUrl` para activar (true) o desactivar (false) el redireccionamiento 302.
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
