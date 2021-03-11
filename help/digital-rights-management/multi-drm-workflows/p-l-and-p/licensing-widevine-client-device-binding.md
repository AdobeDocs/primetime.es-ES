---
description: En algunos casos, es posible que desee restringir el acceso de los usuarios finales a la reproducción de contenido en varios dispositivos cuando el contenido se compra o alquila. Si el cliente utiliza Expressplay, esto se puede hacer utilizando las API de Expression Play para enlazar el token de Expressplay del usuario al equipo del usuario.
title: Enlace de dispositivos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Enlace de dispositivos{#device-binding}

En algunos casos, es posible que desee restringir el acceso de los usuarios finales a la reproducción de contenido en varios dispositivos cuando el contenido se compra o alquila. Si el cliente utiliza Expressplay, esto se puede hacer utilizando las API de Expression Play para enlazar el token de Expressplay del usuario al equipo del usuario.

Puede utilizar las API de la siguiente manera.

1. Genere una cookie.
1. Envíe una solicitud de generación de token ficticio con la cookie generada adjunta como una cadena de consulta (cookie=`<cookie>`) o como encabezados.
1. Pida al equipo del usuario que envíe una solicitud de licencia al servidor de licencias de Expression Play utilizando el token anterior, por ejemplo, reproduciendo un contenido ficticio.

   Esta solicitud de licencia ficticia, cuando se realiza correctamente, asocia el device_id del usuario (calculado o generado por la implementación de DRM en el dispositivo del usuario) a la cookie en el back-end de Expressplay . A continuación, esta cookie se utiliza de la siguiente manera:

   * En el momento de la compra/alquiler del contenido, el código consulta el back-end de Expression play para device_id del usuario enviando la cookie asociada ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * Envíe una solicitud de generación de tokens con la clave (CEK), el keyID (CEKSID), las políticas y otra información del contenido comprado, adjuntando la cookie y el device_id anteriores como, respectivamente, el parámetro de correlación `cookie` y el parámetro de restricción de token `deviceid` respectivamente.

   * Proporcione este token al usuario.

      Este proceso genera un token para el contenido enlazado al device_id del usuario. Cuando el equipo del usuario envía una solicitud de licencia con este token, el back-end de Expressplay comprobará el device_id del token con el device_id de la solicitud de licencia.

      Un servidor de asignación de derechos de expresión de muestra implementa este flujo de trabajo.
