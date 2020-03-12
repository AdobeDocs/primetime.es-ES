---
seo-title: Entrega remota y local de claves de iOS
title: Entrega remota y local de claves de iOS
uuid: 90f672e7-9301-4e14-adca-db2a8f951a83
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Entrega remota y local de claves de iOS {#remote-and-local-ios-key-delivery}

Adobe Primetime admite las siguientes opciones para la entrega de claves a clientes de iOS:

* **Remoto** : se realiza tal como se especifica en la especificación HTTP Live Streaming (HLS); el manifiesto M3U8 especifica una ruta HTTPS que incluye una clave AES que debe utilizarse para descifrar los siguientes segmentos cifrados en el flujo. Cuando especifica `Remote` en la directiva DRM de Primetime, el dispositivo cliente debe conectarse a un servidor HTTPS remoto para obtener una clave AES.

* **Local** : cuando se especifica `Local` en Primetime DRM en lugar de conectarse a Internet/red para la clave AES, se incrusta un servidor HTTPS local en la aplicación iOS, que administra todas las solicitudes clave de AES. El servidor HTTPS incrustado se configura y configura automáticamente en la aplicación P. El desarrollador de la aplicación no requiere ninguna intervención.

La entrega de clave remota se habilita mediante la directiva Primetime DRM que se utiliza para empaquetar contenido. Si desea cambiar esta configuración, debe volver a empaquetar el contenido. Si habilita la entrega remota de claves, debe implementar un servidor de claves de DRM Primetime que pueda administrar las solicitudes clave de los clientes de iOS. Sin embargo, el flujo de trabajo de los clientes no se modifica en otras plataformas.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>La selección de entrega de claves solo afecta a los clientes de iOS. Todos los demás dispositivos que utilizan contenido HLS, como Android y Primetime en el escritorio (Flash Player), siempre utilizan la entrega de `Local` claves, incluso si `Remote` se ha especificado.

