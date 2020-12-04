---
description: Puede convertir cualquiera de los flujos de una aplicación de remitente basada en TVSDK y hacer que el flujo se reproduzca en Chromecast con el TVSDK del explorador.
seo-description: Puede convertir cualquiera de los flujos de una aplicación de remitente basada en TVSDK y hacer que el flujo se reproduzca en Chromecast con el TVSDK del explorador.
seo-title: Aplicación Google Cast para TVSDK de explorador
title: Aplicación Google Cast para TVSDK de explorador
uuid: 018143e2-143a-4f88-97c6-4b10a2083f9e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# Aplicación Google Cast para TVSDK del explorador{#google-cast-app-for-browser-tvsdk}

Puede convertir cualquiera de los flujos de una aplicación de remitente basada en TVSDK y hacer que el flujo se reproduzca en Chromecast con el TVSDK del explorador.

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

Hay dos componentes de una aplicación con función de difusión:

* La aplicación del remitente, que actúa como control remoto.

   Las aplicaciones de envío incluyen teléfonos inteligentes, equipos personales, etc. La aplicación se puede desarrollar con SDK nativos para iOS, Android y Chrome.
* La aplicación receptor, que se ejecuta en Chromecast y reproduce el contenido.

   >[!IMPORTANT]
   >
   >Esta aplicación solo puede ser una aplicación HTML5.

El remitente y el receptor se comunican mediante los SDK de envío para transmitir mensajes.

## Flujo de trabajo básico {#section_FAF680FF29DA4D24A50AC0A2B6402B58}

A continuación se presenta una descripción general del proceso:

1. La aplicación del remitente establece una conexión con la aplicación del receptor.
1. La aplicación del remitente envía un mensaje para cargar los medios en la aplicación del receptor.
1. La aplicación receptor inicia la reproducción.
1. La aplicación del remitente envía mensajes de control de reproducción, como reproducir, pausar, buscar, avanzar rápidamente, rebobinar, rebobinar, cambiar el volumen, etc., a la aplicación del receptor.
1. La aplicación receptora reacciona a estos mensajes.

## Formato del mensaje {#section_1624159DD51D4C87B3E5803DEEBCB6B7}

Debe definir los mensajes para que el remitente y el receptor puedan entenderlos. Este es un ejemplo de un mensaje de búsqueda:

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

Cuando se envían mensajes personalizados, como el mensaje de búsqueda, a través de los SDK de envío, se requiere una Área de nombres de mensaje personalizada. Este es un ejemplo de JavaScript:

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## Establecimiento de una conexión {#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>Las API de TVSDK del explorador no están involucradas al establecer la conexión.

Para establecer una conexión, el remitente y el receptor deben completar las siguientes tareas:

* El remitente debe revisar la documentación de la plataforma en [Desarrollo de la aplicación del remitente](https://developers.google.com/cast/docs/sender_apps).
* El receptor utiliza las API del receptor de envío para establecer una conexión con la aplicación del remitente. Por ejemplo:

   ```js
   window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance(); 
   
   window.castReceiverManager.onReady = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderConnected = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderDisconnected = function (event) { /*handle event*/ }; 
   
   var customMessageBus = window.castReceiverManager.getCastMessageBus(MSG_NAMESPACE); 
   customMessageBus.onMessage = function (event) { /*handle messages*/ }; 
   
   window.castReceiverManager.start(); 
   ```

## Administración de mensajes {#section_3E4814546F5946C9B3E7A1AE384B4FF8}

Para enviar mensajes al receptor, consulte la documentación de la plataforma del remitente.

>[!IMPORTANT]
>
>Debe incluir la Área de nombres de mensaje personalizada, `MSG_NAMESPACE` en todos los mensajes.

Para la aplicación de receptor, siga la documentación de las API de receptor de difusión.

**Ejemplo de un mensaje de remitente basado en Chrome**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**Gestión del Evento del remitente basado en Chrome**

Enlace los controladores de evento a los elementos de interfaz de usuario que enviarán mensajes cuando se activen los eventos correspondientes. Por ejemplo, para una aplicación de remitente basada en Chrome, el evento de búsqueda se puede enviar de esta manera:

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**Gestión de mensajes del receptor**

Desde la aplicación receptor, a continuación se muestra un ejemplo de cómo gestionar el mensaje de búsqueda:

```js
customMessageBus.onMessage = function (event) { 
    var message = JSON.parse(event.data); 
    switch (message.type) { 
        case "seek":  
            player.seek(parseInt(message.seekTo)); 
            break; 
        //code for handling other events 
        default:  
            break; 
    } 
}; 
```

