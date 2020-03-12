---
description: Para reproducir el contenido DASH resultante del empaquetado de contenido, el cliente TVSDK deberá obtener la clave de descifrado de contenido que se pasó durante el proceso de empaquetado en el flujo de trabajo de adquisición de claves. La clave de descifrado de contenido del cliente suele ser entregada al cliente por un servidor de licencias Widevine/PlayReady en respuesta a uno o varios anuncios HTTP/HTTPS del cliente.
seo-description: Para reproducir el contenido DASH resultante del empaquetado de contenido, el cliente TVSDK deberá obtener la clave de descifrado de contenido que se pasó durante el proceso de empaquetado en el flujo de trabajo de adquisición de claves. La clave de descifrado de contenido del cliente suele ser entregada al cliente por un servidor de licencias Widevine/PlayReady en respuesta a uno o varios anuncios HTTP/HTTPS del cliente.
seo-title: Visión general del flujo de trabajo de la solicitud de clave de cliente
title: Visión general del flujo de trabajo de la solicitud de clave de cliente
uuid: 2f01f0ae-adbf-42fa-a908-4b5b9410a26d
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Flujo de trabajo de solicitud de clave de cliente {#client-key-request-workflow-overview}

Para reproducir el contenido DASH resultante del empaquetado de contenido, el cliente TVSDK deberá obtener la clave de descifrado de contenido que se pasó durante el proceso de empaquetado en el flujo de trabajo de adquisición de claves. La clave de descifrado de contenido del cliente suele ser entregada al cliente por un servidor de licencias Widevine/PlayReady en respuesta a uno o varios anuncios HTTP/HTTPS del cliente.

Para adquirir la clave de descifrado de contenido, el cliente PSDK debe hacer lo siguiente

* Tome el cuadro pssh del contenido, dáselo a la plataforma y obtenga una solicitud de clave en respuesta.
* Envíe la solicitud de clave al servidor de licencias Widevine/PlayReady correspondiente mediante HTTP POST.
* Pase la respuesta del servidor a la plataforma que extraerá la clave de descifrado de contenido del cliente de la respuesta y la utilizará para la descodificación de contenido.

Para enviar HTTP POST para la solicitud de clave, el código debe pasar al cliente PSDK la dirección URL del servidor de licencias junto con los datos adicionales que deban adjuntarse al anuncio. La elección de la dirección URL y los datos para pasar depende del proveedor de servicios Widevine/PlayReady con el que trabaje. Por ejemplo, si utiliza ExpressPlay para proporcionar el servicio, transfiere la URL del servidor de licencias ExpressPlay Widevine/PlayReady correspondiente y adjunte a la solicitud de clave saliente el token ExpressPlay asociado con la clave de cifrado del contenido. Puede obtener la URL adecuada del servidor de licencias ExpressPlay Widevine/PlayReady en la documentación de ExpressPlay.