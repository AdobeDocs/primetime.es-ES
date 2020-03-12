---
description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puerta, etc.
seo-description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puerta, etc.
seo-title: Trabajar con cookies
title: Trabajar con cookies
uuid: 7586a5a7-9914-403b-86a9-fbdd28664b07
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Trabajar con cookies{#work-with-cookies}

Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puerta, etc.

A continuación se muestra un ejemplo con algún tipo de autenticación al realizar solicitudes al servidor de claves:

1. El cliente inicia sesión en el sitio web en un navegador y su inicio de sesión muestra que puede ver el contenido.
1. La aplicación genera un autentificador, basado en lo que espera del servidor de licencias. Pase ese valor a TVSDK.
1. TVSDK establece ese valor en el encabezado de la cookie.
1. Cuando TVSDK realiza una solicitud al servidor de claves para obtener una clave para descifrar el contenido, esa solicitud contiene el valor de autenticación en el encabezado de la cookie, de modo que el servidor de claves sabe que la solicitud es válida.

Para trabajar con cookies:

1. Utilice la `cookieHeaders` propiedad de `NetworkConfiguration` para establecer una cookie. La `cookieHeaders` propiedad es un objeto Metadata y puede agregar pares de valor clave a este objeto para incluirlos en el encabezado de la cookie.

   Por ejemplo:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   De forma predeterminada, los encabezados de cookie se envían solo con solicitudes de clave. Para enviar encabezados de cookie con todas las solicitudes, establezca la `NetworkConfiguration` propiedad en `useCookieHeadersForAllRequests` true.

1. Para asegurarse de que `NetworkConfiguration` funciona, configúrelo como metadatos:

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. Proporcione los metadatos del paso anterior cuando cree un `MediaResource`.

   Por ejemplo, si utiliza el `createFromURL` método, introduzca la siguiente información:

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```

