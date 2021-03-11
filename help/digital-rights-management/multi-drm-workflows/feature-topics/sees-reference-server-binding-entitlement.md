---
description: El servidor de referencia SEES le muestra cómo habilitar el servicio de asignación de derechos de enlace de dispositivos mediante ExpressPlay.
title: Derecho de enlace de dispositivos del servicio de referencia
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Servicio de referencia: Derecho de enlace de dispositivos {#reference-service-device-binding-entitlement}

El servidor de referencia SEES le muestra cómo habilitar el servicio de asignación de derechos de enlace de dispositivos mediante ExpressPlay.

>[!NOTE]
>
>El servicio de asignación de derechos dependiente del dispositivo también puede estar sujeto a plazos o proporcionar duración del alquiler.

Para arrancar la información `device_id`, reproduzca un contenido M3U8 ficticio. A continuación, puede incrustar una cookie en el token de ExpressPlay, generar un SPC (que contiene el `device_id`) y enviar un `getToken` al servidor de ExpressPlay.

![](assets/fees-device-binding.png)

La secuencia comienza reproduciendo un M3U8 ficticio. Se envía una cookie al servidor SEES para obtener la URL del token de ExpressPlay. Después de recibir la URL del token ExpressPlay enlazada a cookies, el siguiente paso es generar el SPC y enviarlo al servidor ExpressPlay. El servidor ExpressPlay extrae el `device_id` del SPC, la cookie de la URL del token ExpressPlay y coloca la cookie y `device_id` en el registro de transacciones.

El cliente realiza una solicitud de licencia real a SEES enviando la misma cookie. SEES emplea la cookie para recuperar el `device_id` del servidor de ExpressPlay.

SEES solicita un token ExpressPlay enlazado al dispositivo, así como con tiempo y devuelve ese token al cliente.

El cliente realiza la solicitud de licencia con el token ExpressPlay.

El servidor ExpressPlay compara el `device_id` del RCP con el `device_id` del token ExpressPlay. El servidor ExpressPlay solo emite una licencia si los dos valores `device_id` coinciden.
