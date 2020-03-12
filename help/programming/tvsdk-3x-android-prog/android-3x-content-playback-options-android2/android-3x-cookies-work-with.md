---
description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puerta, etc.
seo-description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puerta, etc.
seo-title: Trabajar con cookies
title: Trabajar con cookies
uuid: 618bc59a-032d-445e-a867-ed2bf260570d
translation-type: tm+mt
source-git-commit: ad58732842eb651514a47dd565e31e3d98a84c46

---


# Trabajar con cookies {#work-with-cookies}

Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puerta, etc.

Esta es una solicitud de muestra al servidor de claves con cierta autenticación:

1. El cliente inicia sesión en el sitio web en un navegador y su inicio de sesión muestra que este cliente puede ver el contenido.
1. Según lo que espera el servidor de licencias, la aplicación genera un autentificador.

   Este valor se pasa a TVSDK.
1. TVSDK establece este valor en el encabezado de la cookie.
1. Cuando TVSDK realiza una solicitud al servidor de claves para obtener una clave para descifrar el contenido, la solicitud contiene el valor de autenticación en el encabezado de la cookie.

   El servidor de claves sabe que la solicitud es válida.

Para trabajar con cookies:

1. Cree un `cookieManager` y agregue las cookies para los URI a su cookieStore.

   Por ejemplo:

   ```java
   CookieManager cookieManager=new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   >[!TIP]
   >
   >Cuando se habilita la redirección 302, la solicitud de publicidad puede redirigirse a un dominio diferente del dominio al que pertenece la cookie.

   TVSDK realiza esta consulta en tiempo de ejecución, comprueba si hay cookies asociadas con la dirección URL y las utiliza automáticamente. `cookieManager`

   Si es necesario actualizar las cookies en la aplicación durante la reproducción, no utilice `networkConfiguration.setCookieHeaders` la API, ya que la actualización se producirá en el almacén de cookies de JAVA.

   `networkConfiguration.setCookieHeaders` La API establece las cookies en C++ CookieStore de TVSDK.

   Al utilizar cookies JAVA y compartirlas entre la aplicación y TVSDK, utilice JAVA CookieStore para administrar las cookies únicamente.

   Antes de iniciar la reproducción, establezca las cookies en CookieStore mediante el Administrador de cookies, como se ha indicado anteriormente.

   TVSDK recogerá automáticamente la cookie almacenada en CookieStore.

   Si es necesario actualizar un valor de cookie más tarde durante la reproducción, llame al mismo método de adición de CookieStore con la misma clave y un nuevo campo de valor.

   También se configura
   `networkConfiguration.setReadSetCookieHeader`(false)antes de llamar
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   Después de establecer &#39;setReadSetCookieHeader&#39; en false, configure las cookies para las solicitudes clave mediante el administrador de cookies JAVA.
   >
   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
Esta API de llamada de retorno se activará cada vez que haya una actualización en las cookies de C++ (cookies que proceden de la respuesta http). La aplicación necesita escuchar esta llamada de retorno y puede actualizar su CookieStore de JAVA según corresponda para que sus llamadas de red en JAVA puedan utilizar las cookies como se muestra a continuación:

   ```
   private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener() {
   @Override
   public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) {
   List<HttpCookie> cookies = cookiesUpdatedEvent.getHttpCookies();
   for(int i = 0; i < cookies.size(); i++)
   { HttpCookie c = cookies.get(i); // To set this cookie on to the cookie store //c.setValue("newValue"); //If you want to modify the value of the cookie URI myuri = URI.create(cookiesUpdatedEvent.getDomainString()); cookieManager.getCookieStore().add(myuri,c); }
   }
   }
   ```
