---
title: Entrega de claves iOS remotas y locales
description: Entrega de claves iOS remotas y locales
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Entrega de claves iOS remotas y locales{#remote-and-local-ios-key-delivery}

Adobe Primetime admite dos opciones para la entrega de claves a clientes de iOS:

* Remoto: exactamente como se especifica en la especificación HLS, el manifiesto M3U8 especifica una ruta HTTPS que contiene una clave AES que debe utilizarse para descifrar los siguientes segmentos cifrados del flujo. Cuando se especifica &quot;Remoto&quot;, el dispositivo cliente se pone en contacto con un servidor HTTPS remoto para recuperar la clave AES.
* Local: cuando se especifica &quot;Local&quot;, en lugar de ponerse en contacto a través de Internet/red para la clave AES, se incrusta un servidor HTTPS local en la aplicación de iOS que administrará todas las solicitudes de claves AES. El servidor HTTPS incrustado se configura y configura automáticamente en la aplicación de Primetime. El desarrollador de aplicaciones no requiere ninguna intervención.

La entrega de claves remotas se habilita a través de la directiva utilizada para empaquetar contenido (para cambiar esta configuración se requiere volver a empaquetar el contenido). Cuando la entrega de claves remotas está habilitada, se debe implementar un servidor de claves de acceso a Adobe para administrar las solicitudes de claves de los clientes de iOS, pero no se ha realizado ningún cambio en el flujo de trabajo de los clientes de otras plataformas.

>[!NOTE]
>
>La selección Entrega de claves solo afecta a los clientes de iOS. Todos los demás dispositivos que consuman contenido HLS siempre utilizarán la entrega de claves &quot;Local&quot;, incluso si se ha especificado &quot;Remoto&quot;.

Para obtener más información, consulte *Uso del servidor de claves de acceso a Adobe*.
