---
description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puertas, etc.
title: Trabajo con cookies
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Trabajo con cookies {#work-with-cookies}

Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puertas, etc.

Esta es una solicitud de ejemplo al servidor de claves con algo de autenticación:

1. El cliente inicia sesión en el sitio web en un explorador y su inicio de sesión muestra que este cliente tiene permiso para ver contenido.
1. En función de lo que espere el servidor de licencias, la aplicación generará un token de autenticación.

   Este valor se pasa a TVSDK.
1. TVSDK establece este valor en el encabezado de la cookie.
1. Cuando TVSDK realiza una solicitud al servidor de claves para obtener una clave para descifrar el contenido, la solicitud contiene el valor de autenticación en el encabezado de la cookie.

   El servidor de claves sabe que la solicitud es válida.

Para trabajar con cookies:

1. Crear un `cookieManager` y añada sus cookies para los URI de su cookieStore.

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
   >Cuando la redirección 302 está habilitada, la solicitud de publicidad se puede redirigir a un dominio diferente del dominio al que pertenece la cookie.

   TVSDK consulta esto `cookieManager` en tiempo de ejecución, comprueba si hay cookies asociadas a la dirección URL y las utiliza automáticamente.

   Si es necesario actualizar las cookies en la aplicación durante la reproducción, no utilice `networkConfiguration.setCookieHeaders` API, ya que la actualización se producirá en el almacén de cookies JAVA.

   `networkConfiguration.setCookieHeaders` La API establece las cookies en el almacén de cookies de C++ de TVSDK.

   Cuando utilice cookies JAVA y las comparta entre Application y TVSDK, utilice JAVA CookieStore para gestionar las cookies únicamente.

   Antes de iniciar la reproducción, establezca las cookies en CookieStore mediante el Administrador de cookies como se ha indicado anteriormente.

   TVSDK recoge automáticamente la cookie almacenada en CookieStore.

   Si es necesario actualizar un valor de cookie más adelante durante la reproducción, llame al mismo método add de CookieStore con la misma clave y un nuevo campo de valor.

   También establecido
   `networkConfiguration.setReadSetCookieHeader`(false) antes de llamar a
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >Después de establecer este &quot;setReadSetCookieHeader&quot; en false, establezca las cookies para las solicitudes de clave mediante el administrador de cookies JAVA.

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
Esta API de llamada de retorno se activa siempre que haya una actualización en las cookies de C++ (cookies que provienen de la respuesta http). La aplicación debe escuchar esta llamada de retorno y puede actualizar su JAVA CookieStore en consecuencia para que sus llamadas de red en JAVA puedan utilizar las cookies como se muestra a continuación:

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
