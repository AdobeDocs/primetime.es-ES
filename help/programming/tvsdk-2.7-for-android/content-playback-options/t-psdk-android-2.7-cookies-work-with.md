---
description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookies para la administración de sesiones, el acceso a puertas, etc.
title: Trabajo con cookies
exl-id: ea9d83f9-a047-4e24-98e5-f565b8a31a89
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '236'
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

Crear un `cookieManager` y añada sus cookies para los URI de su cookieStore.

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

Se llama al evento MediaPlayerEvent.COOKIES_UPDATED cuando se actualizan las cookies de C++. Este cookieUpdatedEvent tiene un método getCookieString() que devuelve un valor de cadena para la cookie.

A continuación se muestra un fragmento de código de ejemplo:

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
