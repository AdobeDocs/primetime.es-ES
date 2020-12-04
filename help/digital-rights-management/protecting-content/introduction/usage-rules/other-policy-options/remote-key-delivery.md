---
seo-title: Envío de claves de iOS local y remota
title: Envío de claves de iOS local y remota
uuid: 90f672e7-9301-4e14-adca-db2a8f951a83
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Envío de clave remota y local de iOS {#remote-and-local-ios-key-delivery}

Adobe Primetime admite las siguientes opciones de envío clave para clientes iOS:

* **Remoto** : se realiza tal como se especifica en la especificación HTTP Live Streaming (HLS); el manifiesto M3U8 especifica una ruta HTTPS que incluye una clave AES que debe utilizarse para descifrar los siguientes segmentos cifrados en el flujo. Cuando especifica `Remote` en la directiva DRM de Primetime, el dispositivo cliente debe conectarse a un servidor HTTPS remoto para obtener una clave AES.

* **Local** : cuando se especifica  `Local` en Primetime DRM en lugar de conectarse a Internet/red para la clave AES, se incrusta un servidor HTTPS local en la aplicación iOS, que luego administra todas las solicitudes clave AES. El servidor HTTPS incrustado se configura y configura automáticamente en la aplicación P. El desarrollador de la aplicación no requiere ninguna intervención.

El envío de clave remota se habilita mediante la directiva Primetime DRM que se utiliza para empaquetar contenido. Si desea cambiar esta configuración, debe volver a empaquetar el contenido. Si habilita el envío de claves remotas, debe implementar un servidor de claves DRM Primetime que pueda administrar las solicitudes clave de los clientes de iOS. Sin embargo, el flujo de trabajo de los clientes no se modifica en otras plataformas.

>[!NOTE]
>
>La selección de envíos clave solo afecta a los clientes de iOS. Todos los demás dispositivos que utilizan contenido HLS, como Android y Primetime en el escritorio (Flash Player), siempre utilizan el envío clave `Local`, aunque se haya especificado `Remote`.

