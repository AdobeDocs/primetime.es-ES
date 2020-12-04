---
description: El servidor de referencia SEES le muestra cómo activar el servicio de asignación de derechos de enlace de dispositivo mediante ExpressPlay.
seo-description: El servidor de referencia SEES le muestra cómo activar el servicio de asignación de derechos de enlace de dispositivo mediante ExpressPlay.
seo-title: Asignación de derechos de enlace de dispositivos del servicio de referencia
title: Asignación de derechos de enlace de dispositivos del servicio de referencia
uuid: 22ce2f8e-1758-4528-8caf-60d209839afe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Servicio de referencia: Asignación de derechos de enlace de dispositivo {#reference-service-device-binding-entitlement}

El servidor de referencia SEES le muestra cómo activar el servicio de asignación de derechos de enlace de dispositivo mediante ExpressPlay.

>[!NOTE]
>
>El servicio de asignación de derechos con destino a dispositivo también puede estar sujeto a plazos o proporcionar duración de alquiler.

Para arrancar la información `device_id`, reproduzca un contenido M3U8 ficticio. A continuación, puede incrustar una cookie en el token de ExpressPlay, generar un SPC (que contiene el `device_id`) y enviar un `getToken` al servidor de ExpressPlay.

![](assets/fees-device-binding.png)

La secuencia inicio al reproducir un maniquí M3U8. Se envía una cookie al servidor SEES para obtener la URL del token de ExpressPlay. Después de recibir la URL del token ExpressPlay enlazada a una cookie, el siguiente paso es generar el SPC y enviarlo al servidor ExpressPlay. El servidor ExpressPlay extrae el `device_id` de SPC, la cookie de la URL del token de ExpressPlay y coloca la cookie y `device_id` en el registro de transacciones.

El cliente realiza una solicitud de licencia real a SEES enviando la misma cookie. SEES emplea la cookie para recuperar `device_id` del servidor ExpressPlay.

SEES solicita un token de ExpressPlay que está enlazado al dispositivo y a tiempo y devuelve dicho token al cliente.

El cliente realiza la solicitud de licencia con el token de ExpressPlay.

El servidor ExpressPlay compara el `device_id` del RCP con el `device_id` del token de ExpressPlay. El servidor ExpressPlay solo emite una licencia si coinciden los dos valores `device_id`.
