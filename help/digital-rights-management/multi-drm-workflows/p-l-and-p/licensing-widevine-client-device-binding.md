---
description: En algunos casos, es posible que desee restringir la reproducción de contenido por parte de los usuarios finales en varios dispositivos cuando el contenido se compra o se alquila. Si el cliente utiliza ExpressPlay, esto se puede hacer mediante las API de ExpressPlay para enlazar el token de Expressplay del usuario al equipo del usuario.
seo-description: En algunos casos, es posible que desee restringir la reproducción de contenido por parte de los usuarios finales en varios dispositivos cuando el contenido se compra o se alquila. Si el cliente utiliza ExpressPlay, esto se puede hacer mediante las API de ExpressPlay para enlazar el token de Expressplay del usuario al equipo del usuario.
seo-title: Enlace de dispositivos
title: Enlace de dispositivos
uuid: 351fa33c-4226-4ed5-829c-56b563166fec
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Enlace de dispositivos{#device-binding}

En algunos casos, es posible que desee restringir la reproducción de contenido por parte de los usuarios finales en varios dispositivos cuando el contenido se compra o se alquila. Si el cliente utiliza ExpressPlay, esto se puede hacer mediante las API de ExpressPlay para enlazar el token de Expressplay del usuario al equipo del usuario.

Puede usar las API de la siguiente manera.

1. Genere una cookie.
1. Envíe una solicitud de generación de token ficticio con la cookie generada adjunta como una cadena de consulta (cookie=`<cookie>`) o como encabezados.
1. Pida al equipo del usuario que envíe una solicitud de licencia al servidor de licencias de ExpressPlay mediante el token anterior, por ejemplo reproduciendo un contenido ficticio.

   Esta solicitud de licencia ficticia, cuando se realiza correctamente, asocia el device_id del usuario (calculado o generado por la implementación de DRM en el dispositivo del usuario) a la cookie del back-end de Expressplay. Esta cookie se utiliza de la siguiente manera:

   * En el momento de la compra/alquiler de contenido, el código consulta el back-end de la reproducción de expresiones para el device_id del usuario enviando la cookie asociada ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * Envíe una solicitud de generación de tokens con la clave del contenido adquirido (CEK), keyID (CEKSID), políticas y otra información, adjuntando la cookie y el device_id anteriores como, respectivamente, parámetro de `cookie` correlación y parámetro de restricción de `deviceid` tokens.

   * Proporcione este token al usuario.

      Este proceso genera un token para el contenido enlazado al device_id del usuario. Cuando el equipo del usuario envía una solicitud de licencia con este distintivo, el back-end de Expressplay verificará el device_id del token con el device_id de la solicitud de licencia.

      Un servidor de asignación de derechos de muestra de Expressplay implementa este flujo de trabajo.
