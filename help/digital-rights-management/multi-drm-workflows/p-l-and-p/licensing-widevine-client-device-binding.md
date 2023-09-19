---
description: En algunos casos, es posible que desee restringir el acceso de los usuarios finales a la reproducción de contenido en varios dispositivos cuando se compre o alquile el contenido. Si el cliente utiliza Expressplay, esto se puede hacer mediante las API de Expressplay para enlazar el token de Expressplay del usuario al equipo del usuario.
title: Enlace de dispositivo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Enlace de dispositivo{#device-binding}

En algunos casos, es posible que desee restringir el acceso de los usuarios finales a la reproducción de contenido en varios dispositivos cuando se compre o alquile el contenido. Si el cliente utiliza Expressplay, esto se puede hacer mediante las API de Expressplay para enlazar el token de Expressplay del usuario al equipo del usuario.

Puede utilizar las API de las siguientes maneras.

1. Genere una cookie.
1. Envíe una solicitud de generación de token ficticio con la cookie generada adjunta como cadena de consulta (cookie=`<cookie>`) o como encabezados.
1. Haga que el equipo del usuario envíe una solicitud de licencia al servidor de licencias de Expressplay utilizando el token anterior, por ejemplo reproduciendo contenido ficticio.

   Cuando se realiza correctamente, esta solicitud de licencia ficticia asocia el device_id del usuario (calculado o generado por la implementación de DRM en el dispositivo del usuario) a la cookie en el back-end de Expressplay. Esta cookie se utiliza de la siguiente manera:

   * En el momento de la compra/alquiler de contenido, el código consulta el back-end Expressplay para el device_id del usuario enviando la cookie asociada ( [https://www.expressplay.com/developer/restapi/#record-retrieval](https://www.expressplay.com/developer/restapi/#record-retrieval))
   * Envíe una solicitud de generación de tokens con la clave (CEK), el identificador de clave (CEKSID), las directivas y otra información del contenido comprado, adjuntando la cookie y el identificador de dispositivo anteriores como, respectivamente, el `cookie` parámetro de correlación y `deviceid` parámetro de restricción de token.

   * Proporcione este token al usuario.

     Este proceso genera un token para el contenido enlazado al device_id del usuario. Cuando el equipo del usuario envía una solicitud de licencia con este token, el back-end de Expressplay comprobará el device_id del token con el device_id de la solicitud de licencia.

     Este flujo de trabajo se implementa mediante un servidor de derechos de Expressplay de ejemplo.
