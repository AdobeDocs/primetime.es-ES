---
description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookie para la administración de sesiones, el acceso a la puerta, etc.
title: Trabajar con cookies
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Trabajar con cookies{#work-with-cookies}

Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookie para la administración de sesiones, el acceso a la puerta, etc.

A continuación, se muestra un ejemplo con algún tipo de autenticación al realizar solicitudes al servidor de claves:

1. El cliente inicia sesión en el sitio web en un explorador y su inicio de sesión muestra que puede ver el contenido.
1. La aplicación genera un token de autenticación, en función de lo que espera el servidor de licencias. Pase ese valor a TVSDK.
1. TVSDK establece ese valor en el encabezado de la cookie.
1. Cuando TVSDK realiza una solicitud al servidor de claves para obtener una clave para descifrar el contenido, esa solicitud contiene el valor de autenticación en el encabezado de la cookie, por lo que el servidor de claves sabe que la solicitud es válida.

Para trabajar con cookies:

1. Cree un `cookieManager` y añada las cookies para los URI a su `cookieStore`.

   Por ejemplo:

   >[!IMPORTANT]
   >
   >Cuando se habilita el redireccionamiento 302, la solicitud de publicidad puede redirigirse a un dominio diferente del dominio al que pertenece la cookie.

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK consulta este cookieManager durante la ejecución, comprueba si hay cookies asociadas con la dirección URL y las utiliza automáticamente.

   Otra opción es utilizar `cookieHeaders` en `NetworkConfiguration` para establecer una cadena de encabezado de cookie arbitraria que se utilizará para las solicitudes. De forma predeterminada, este encabezado de cookie se envía solo con solicitudes clave. Para enviar el encabezado de la cookie con todas las solicitudes, utilice el método `NetworkConfiguration` `setUseCookieHeadersForAllRequests`:

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
