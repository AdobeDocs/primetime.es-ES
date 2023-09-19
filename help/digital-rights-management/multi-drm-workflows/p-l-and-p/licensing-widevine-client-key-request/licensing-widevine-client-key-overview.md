---
description: Para reproducir el contenido DASH resultante del empaquetado de contenido, el cliente TVSDK deberá obtener la clave de descifrado de contenido que se pasó durante el proceso de empaquetado en el flujo de trabajo de adquisición de claves. La clave de descifrado de contenido del cliente se suele entregar al cliente mediante un servidor de licencias Widevine/PlayReady en respuesta a una o varias publicaciones HTTP/HTTPS del cliente.
title: Resumen del flujo de trabajo Solicitud de clave de cliente
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Flujo de trabajo de solicitud de clave de cliente {#client-key-request-workflow-overview}

Para reproducir el contenido DASH resultante del empaquetado de contenido, el cliente TVSDK deberá obtener la clave de descifrado de contenido que se pasó durante el proceso de empaquetado en el flujo de trabajo de adquisición de claves. La clave de descifrado de contenido del cliente se suele entregar al cliente mediante un servidor de licencias Widevine/PlayReady en respuesta a una o varias publicaciones HTTP/HTTPS del cliente.

Para adquirir la clave de descifrado de contenido, el cliente PSDK debe hacer lo siguiente

* Tome el cuadro pssh del contenido, entréguelo a la plataforma y obtenga una solicitud de clave como respuesta.
* Envíe la solicitud de clave al servidor de licencias apropiado de Widevine/PlayReady a través de un POST HTTP.
* Pase la respuesta del servidor a la plataforma que extraerá la clave de descifrado de contenido del cliente de la respuesta y la utilizará para el descifrado de contenido.

Para enviar el POST HTTP para la solicitud de clave, el código debe pasar al cliente PSDK la URL del servidor de licencias junto con los datos adicionales que deban adjuntarse a la publicación. La elección de la dirección URL y los datos que se van a pasar depende del proveedor de servicios Widevine/PlayReady con el que trabaje. Por ejemplo, si utiliza ExpressPlay para proporcionar el servicio, pasa la URL del servidor de licencias de ExpressPlay Widevine/PlayReady correspondiente y adjunta a la solicitud de clave saliente el token de ExpressPlay asociado con la clave de cifrado del contenido. Puede obtener la URL del servidor de licencias ExpressPlay Widevine/PlayReady adecuada desde la documentación de ExpressPlay.
