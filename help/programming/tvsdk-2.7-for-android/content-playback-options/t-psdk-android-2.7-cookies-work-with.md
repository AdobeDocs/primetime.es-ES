---
description: Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookie para la administración de sesiones, el acceso a la puerta, etc.
title: Trabajar con cookies
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Trabajar con cookies {#work-with-cookies}

Puede utilizar TVSDK para enviar datos arbitrarios en encabezados de cookie para la administración de sesiones, el acceso a la puerta, etc.

A continuación, se muestra un ejemplo de solicitud al servidor de claves con cierta autenticación:

1. El cliente inicia sesión en el sitio web en un explorador y su inicio de sesión muestra que este cliente puede ver el contenido.
1. En función de lo que espera el servidor de licencias, la aplicación genera un token de autenticación.

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
>Cuando se habilita el redireccionamiento 302, la solicitud de publicidad puede redirigirse a un dominio diferente del dominio al que pertenece la cookie.

TVSDK consulta esto `cookieManager` durante la ejecución, comprueba si hay cookies asociadas con la dirección URL y las utiliza automáticamente.

Se llama al evento MediaPlayerEvent.COOKIES_UPDATED cuando se actualizan las cookies C++. Este cookieUpdatedEvent tiene un método getCookieString() que devuelve un valor de cadena para la cookie.

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

