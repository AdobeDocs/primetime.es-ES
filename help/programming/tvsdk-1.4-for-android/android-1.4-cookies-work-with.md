---
description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puertas, etc.
title: Trabajo con cookies
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '246'
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

1. Crear un `cookieManager` y añada sus cookies para los URI a su `cookieStore`.

   Por ejemplo:

   >[!IMPORTANT]
   >
   >Cuando la redirección 302 está habilitada, la solicitud de publicidad se puede redirigir a un dominio diferente del dominio al que pertenece la cookie.

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK consulta este cookieManager durante la ejecución, comprueba si hay cookies asociadas a la dirección URL y las utiliza automáticamente.

   Otra opción es utilizar `cookieHeaders` in `NetworkConfiguration` para establecer una cadena de encabezado de cookie arbitraria para usarla en las solicitudes. De forma predeterminada, este encabezado de cookie se envía solo con solicitudes de clave. Para enviar el encabezado de la cookie con todas las solicitudes, utilice el `NetworkConfiguration` método `setUseCookieHeadersForAllRequests`:

```java
   NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
    
   Metadata cookie = new MetadataNode(); 
   cookie.setValue("reqPayload", “1234567”); 
   networkConfiguration.setCookieHeaders(cookie); 
   networkConfiguration.setUseCookieHeadersForAllRequests( true ); 
    
   // Set NetworkConfiguration as Metadata:                                                                   
   MetadataNode resourceMetadata = new MetadataNode(); 
   resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                            networkConfiguration); 
    
   // Call MediaResource.createFromURL to set the metadata: 
   MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
   // Load the resource 
   mediaPlayer.replaceCurrentItem(resource);
```
