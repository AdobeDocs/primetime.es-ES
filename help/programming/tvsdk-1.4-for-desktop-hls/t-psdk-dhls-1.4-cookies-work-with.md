---
description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puertas, etc.
title: Trabajo con cookies
exl-id: f7a64c77-7db6-4bae-b299-69267fedc673
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Trabajo con cookies{#work-with-cookies}

Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puertas, etc.

Este es un ejemplo con algún tipo de autenticación al realizar solicitudes al servidor de claves:

1. El cliente inicia sesión en el sitio web en un explorador y su inicio de sesión muestra que puede ver contenido.
1. La aplicación genera un token de autenticación basado en lo que espera el servidor de licencias. Pase ese valor a TVSDK.
1. TVSDK establece ese valor en el encabezado de la cookie.
1. Cuando TVSDK realiza una solicitud al servidor de claves para obtener una clave para descifrar el contenido, esa solicitud contiene el valor de autenticación en el encabezado de la cookie, de modo que el servidor de claves sabe que la solicitud es válida.

Para trabajar con cookies:

1. Utilice el `cookieHeaders` propiedad en `NetworkConfiguration` para establecer una cookie. El `cookieHeaders` La propiedad es un objeto Metadata y se pueden añadir pares de valor clave a este objeto para incluirlos en el encabezado de la cookie.

   Por ejemplo:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   De forma predeterminada, los encabezados de cookie solo se envían con solicitudes de clave. Para enviar encabezados de cookies con todas las solicitudes, establezca `NetworkConfiguration` propiedad `useCookieHeadersForAllRequests` a true.

1. Para garantizar que `NetworkConfiguration` funciona, configúrelo como metadatos:

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. Proporcione los metadatos del paso anterior cuando cree un `MediaResource`.

   Por ejemplo, si utiliza la variable `createFromURL` método, introduzca la siguiente información:

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```
