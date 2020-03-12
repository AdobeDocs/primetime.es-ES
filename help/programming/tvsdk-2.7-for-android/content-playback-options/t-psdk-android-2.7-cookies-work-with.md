---
description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puerta, etc.
seo-description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puerta, etc.
seo-title: Trabajar con cookies
title: Trabajar con cookies
uuid: a3b966fd-1263-458d-8303-b4e898372ee1
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

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

Cree un `cookieManager` y agregue las cookies para los URI a su cookieStore.

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

Se llama al evento MediaPlayerEvent.COOKIES_UPDATED cuando se actualizan las cookies de C++. Este cookieUpdatedEvent tiene un método getCookieString() que devuelve un valor de cadena para la cookie.

A continuación se muestra un fragmento de código de muestra:

```
private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener()  
{ 
@Override 
public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) 
 { 
 String cookieStr = cookiesUpdatedEvent.getCookieString();  
 logger.i(LOG_TAG + "::MediaPlayer.CookiesUpdatedEventListener#onCookiesUpdated()", "cookieStr " + cookieStr);  
 }  
};
```

