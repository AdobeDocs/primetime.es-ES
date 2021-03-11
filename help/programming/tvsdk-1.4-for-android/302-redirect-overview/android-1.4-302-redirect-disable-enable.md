---
description: La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a su aplicación equilibrar la carga de manera más efectiva.
title: Deshabilitar o habilitar la optimización de redireccionamiento 302
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 1%

---


# Optimización de redireccionamiento HTTP 302 {#http-302-redirect-optimization}

La optimización de redireccionamiento 302 minimiza el número de 302 respuestas de redireccionamiento, lo que permite a su aplicación equilibrar la carga de manera más efectiva.

Si se redirige una solicitud de manifiesto principal y se habilita la optimización 302 en el reproductor, las solicitudes posteriores realizadas para los recursos desde ese manifiesto utilizarán la ubicación de dominio final, lo que evita respuestas adicionales 302.

Esta función está habilitada de forma predeterminada y puede cambiar esta configuración.

## Deshabilitar o habilitar la optimización de redireccionamiento 302{#disable-or-enable-redirect-optimization}

Utilice la propiedad `useRedirectedUrl` para activar o desactivar el redireccionamiento 302 (true) o (false).
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

