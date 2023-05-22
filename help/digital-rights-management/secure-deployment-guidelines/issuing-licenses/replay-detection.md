---
description: La protección de reproducción evita que un atacante reproduzca un mensaje de solicitud de licencia y que pueda provocar un ataque de denegación de servicio (DoS) contra el cliente.
title: Protección de repetición
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Protección de repetición{#replay-protection}

La protección de reproducción evita que un atacante reproduzca un mensaje de solicitud de licencia y que pueda provocar un ataque de denegación de servicio (DoS) contra el cliente.

Un ataque DoS es un intento de los atacantes de impedir que los usuarios legítimos de un servicio utilicen ese servicio. Por ejemplo, un ataque de reproducción que utilice el contador de reversión podría utilizarse para &quot;engañar&quot; al servidor de licencias y hacer pensar que el cliente DRM ha revertido su estado, lo que provoca una suspensión de la cuenta.

Para obtener más información acerca de la protección de reproducción, consulte [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).
