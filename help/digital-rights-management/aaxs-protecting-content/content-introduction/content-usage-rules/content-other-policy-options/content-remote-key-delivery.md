---
seo-title: Envío de claves de iOS local y remota
title: Envío de claves de iOS local y remota
uuid: 3c20b1d1-f842-438a-ae3a-4ec31da306ad
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Envío de claves de iOS local y remota{#remote-and-local-ios-key-delivery}

Adobe Primetime admite dos opciones de envío clave para clientes iOS:

* Remoto: tal como se especifica en la especificación HLS, el manifiesto M3U8 especifica una ruta HTTPS que contiene una clave AES que debe utilizarse para descifrar los siguientes segmentos cifrados en el flujo. Cuando se especifica &quot;Remoto&quot;, el dispositivo cliente se conecta a un servidor HTTPS remoto para recuperar la clave AES.
* Local: cuando se especifica &quot;Local&quot;, en lugar de conectarse a través de Internet o de la red para la clave AES, se incrusta un servidor HTTPS local en la aplicación iOS que gestionará todas las solicitudes clave de AES. El servidor HTTPS incrustado se configura y configura automáticamente en la aplicación Primetime. El desarrollador de la aplicación no requiere ninguna intervención.

El envío de clave remota se habilita a través de la directiva utilizada para empaquetar contenido (para cambiar esta configuración es necesario volver a empaquetar el contenido). Cuando se habilita el envío de clave remota, se debe implementar un servidor de claves de acceso de Adobe para gestionar solicitudes clave de clientes de iOS, pero no se produce ningún cambio en el flujo de trabajo de los clientes de otras plataformas.

>[!NOTE]
>
>La selección de envíos clave solo afecta a los clientes de iOS. Todos los demás dispositivos que consuman contenido HLS siempre utilizarán el envío de claves &quot;Local&quot;, incluso si se ha especificado &quot;Remoto&quot;.

Para obtener más información, consulte *Uso del servidor* de claves de acceso a Adobe.
