---
title: Entrega remota y local de claves de iOS
description: Entrega remota y local de claves de iOS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Entrega de claves iOS remotas y locales {#remote-and-local-ios-key-delivery}

Adobe Primetime admite las siguientes opciones para la entrega de claves a clientes de iOS:

* **Remoto** : funciona tal como se especifica en la especificación HTTP Live Streaming (HLS); el manifiesto M3U8 especifica una ruta HTTPS que incluye una clave AES que debe utilizarse para descifrar los siguientes segmentos cifrados en el flujo. Cuando especifica `Remote` en la directiva de DRM de Primetime, el dispositivo cliente debe conectarse a un servidor HTTPS remoto para obtener una clave AES.

* **Local** : cuando especifica  `Local` en el DRM de Primetime en lugar de conectarse a Internet/red para la clave de AES, un servidor HTTPS local se incrusta en la aplicación de iOS, que luego administra todas las solicitudes clave de AES. El servidor HTTPS incrustado se configura y configura automáticamente en la aplicación P. El desarrollador de la aplicación no requiere ninguna intervención.

La entrega de clave remota se habilita a través de la directiva Primetime DRM que se utiliza para empaquetar contenido. Si desea cambiar esta configuración, debe volver a empaquetar el contenido. Si habilita la entrega de claves remotas, debe implementar un Servidor de claves DRM de Primetime que pueda administrar las solicitudes clave de los clientes de iOS. Sin embargo, no hay ningún cambio en el flujo de trabajo de los clientes en otras plataformas.

>[!NOTE]
>
>La selección de envíos clave solo afecta a los clientes de iOS. Todos los demás dispositivos que utilizan contenido HLS, como Android y Primetime on Desktop (Flash Player), siempre utilizan la entrega de claves `Local`, aunque se haya especificado `Remote`.

