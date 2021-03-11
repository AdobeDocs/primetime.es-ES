---
title: Entrega de claves iOS locales y remotas
description: Entrega de claves iOS locales y remotas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Entrega de claves iOS remotas y locales{#remote-and-local-ios-key-delivery}

Adobe Primetime admite dos opciones para la entrega de claves a clientes de iOS:

* Remoto: exactamente como se especifica en la especificación HLS, el manifiesto M3U8 especifica una ruta HTTPS que contiene una clave AES que debe utilizarse para descifrar los siguientes segmentos cifrados en el flujo. Cuando se especifica &quot;Remoto&quot;, el dispositivo cliente se pondrá en contacto con un servidor HTTPS remoto para recuperar la clave AES.
* Local : cuando se especifica &quot;Local&quot;, en lugar de conectarse a través de Internet/red para la clave AES, se incrusta un servidor HTTPS local en la aplicación de iOS que gestiona todas las solicitudes clave de AES. El servidor HTTPS incrustado se configura y configura automáticamente en la aplicación Primetime. El desarrollador de la aplicación no requiere ninguna intervención.

La entrega de clave remota se habilita mediante la directiva utilizada para empaquetar contenido (para cambiar esta configuración es necesario volver a empaquetar el contenido). Cuando la entrega de claves remotas está habilitada, se debe implementar un servidor de claves de acceso a Adobe para gestionar solicitudes clave de clientes de iOS, pero no se ha cambiado el flujo de trabajo de los clientes en otras plataformas.

>[!NOTE]
>
>La selección de envíos clave solo afecta a los clientes de iOS. Todos los demás dispositivos que consumen contenido HLS siempre utilizarán la entrega de claves &quot;Local&quot;, incluso si se ha especificado &quot;Remoto&quot;.

Para obtener más información, consulte *Uso del servidor de claves de acceso al Adobe*.
