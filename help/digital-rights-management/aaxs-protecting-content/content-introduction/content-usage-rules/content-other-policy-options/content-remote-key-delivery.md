---
seo-title: Entrega remota y local de claves de iOS
title: Entrega remota y local de claves de iOS
uuid: 3c20b1d1-f842-438a-ae3a-4ec31da306ad
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Entrega remota y local de claves de iOS{#remote-and-local-ios-key-delivery}

Adobe Primetime admite dos opciones para la entrega de claves a clientes de iOS:

* Remoto: tal como se especifica en la especificación HLS, el manifiesto M3U8 especifica una ruta HTTPS que contiene una clave AES que debe utilizarse para descifrar los siguientes segmentos cifrados en el flujo. Cuando se especifica &quot;Remoto&quot;, el dispositivo cliente se conecta a un servidor HTTPS remoto para recuperar la clave AES.
* Local: cuando se especifica &quot;Local&quot;, en lugar de conectarse a través de Internet o de la red para la clave AES, se incrusta un servidor HTTPS local en la aplicación iOS que gestionará todas las solicitudes clave de AES. El servidor HTTPS incrustado se configura y configura automáticamente en la aplicación Primetime. El desarrollador de la aplicación no requiere ninguna intervención.

La entrega de clave remota se habilita mediante la directiva utilizada para empaquetar contenido (para cambiar esta configuración es necesario volver a empaquetar el contenido). Cuando la entrega de clave remota está habilitada, se debe implementar un servidor de claves de Adobe Access para gestionar las solicitudes clave de los clientes de iOS, pero no hay cambios en el flujo de trabajo para los clientes de otras plataformas.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>La selección de entrega de claves solo afecta a los clientes de iOS. Todos los demás dispositivos que consuman contenido HLS siempre utilizarán la entrega de claves &quot;local&quot;, incluso si se ha especificado &quot;remoto&quot;.

Para obtener más información, consulte *Uso del servidor* de claves de Adobe Access.
