---
description: La protección de reproducción evita que un atacante vuelva a reproducir un mensaje de solicitud de licencia y pueda causar un ataque de denegación de servicio (DoS) contra el cliente.
seo-description: La protección de reproducción evita que un atacante vuelva a reproducir un mensaje de solicitud de licencia y pueda causar un ataque de denegación de servicio (DoS) contra el cliente.
seo-title: Protección contra repetición
title: Protección contra repetición
uuid: 93749dd3-a42c-4866-ac54-1b20d6683c42
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Protección contra repetición{#replay-protection}

La protección de reproducción evita que un atacante vuelva a reproducir un mensaje de solicitud de licencia y pueda causar un ataque de denegación de servicio (DoS) contra el cliente.

Un ataque DoS es un intento de los atacantes de evitar que los usuarios legítimos de un servicio usen ese servicio. Por ejemplo, un ataque de reproducción que utilice el contador de reversión podría utilizarse para &quot;engañar&quot; al servidor de licencias para que piense que el cliente de DRM ha revertido su estado, lo que provoca una suspensión de la cuenta.

Para obtener más información sobre la protección contra la reproducción, consulte [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).
