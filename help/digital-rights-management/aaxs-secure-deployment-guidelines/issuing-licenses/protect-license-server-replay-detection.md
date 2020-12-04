---
seo-title: Protección contra repetición
title: Protección contra repetición
uuid: 5e6488e6-0834-4dcf-bc26-55019f5db320
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Reproducir protección{#replay-protection}

La protección de reproducción evita que un atacante vuelva a reproducir un mensaje de solicitud de licencia y pueda causar un ataque de denegación de servicio (DoS) contra el cliente (Un *ataque de denegación de servicio* es un intento de los atacantes de evitar que los usuarios legítimos de un servicio utilicen ese servicio). Por ejemplo, un ataque de reproducción que utilice el contador de reversión podría utilizarse para &quot;engañar&quot; al servidor de licencias para que piense que el cliente DRM está revirtiendo su estado, lo que provocaría una suspensión de la cuenta.

Para obtener más información sobre la protección de repetición, consulte `AbstractRequestMessage.getMessageId()` la *Referencia de API de acceso a Adobe*.
