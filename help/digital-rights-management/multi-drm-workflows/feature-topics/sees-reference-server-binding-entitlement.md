---
description: El servidor de referencia SEES muestra cómo habilitar el servicio de asignación de derechos de enlace de dispositivos mediante ExpressPlay.
title: Derecho de enlace de dispositivo del servicio de referencia
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Servicio de referencia: derecho de enlace de dispositivo {#reference-service-device-binding-entitlement}

El servidor de referencia SEES muestra cómo habilitar el servicio de asignación de derechos de enlace de dispositivos mediante ExpressPlay.

>[!NOTE]
>
>El servicio de derechos enlazado al dispositivo también puede tener un límite de tiempo o proporcionar la duración del alquiler.

Para arrancar el `device_id` información, reproducir un contenido M3U8 ficticio. A continuación, puede incrustar una cookie en el token de ExpressPlay y generar un SPC (que contiene el `device_id`) y envíe un `getToken` al servidor ExpressPlay.

![](assets/fees-device-binding.png)

La secuencia comienza reproduciendo un M3U8 ficticio. Se envía una cookie al servidor SEES para obtener la URL del token de ExpressPlay. Después de recibir la URL del token de ExpressPlay enlazado a cookies, el siguiente paso es generar el SPC y enviarlo al servidor de ExpressPlay. El servidor ExpressPlay extrae el `device_id` en SPC, la cookie de la URL del token de ExpressPlay, y coloca la cookie y `device_id` en el registro de transacciones.

El cliente realiza una solicitud de licencia real a SEES enviando la misma cookie. SEES emplea la cookie para recuperar el `device_id` del servidor ExpressPlay.

SEES solicita un token de ExpressPlay enlazado al dispositivo y al tiempo, y lo devuelve al cliente.

El cliente realiza la solicitud de licencia con el token de ExpressPlay.

El servidor ExpressPlay compara el `device_id` en el RCP con el `device_id` en el token de ExpressPlay. El servidor ExpressPlay solo emite una licencia si los dos `device_id` Los valores de coinciden.
