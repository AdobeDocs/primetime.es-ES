---
title: Protección contra repetición
description: Protección contra repetición
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Reproducir protección{#replay-protection}

La protección contra repetición impide que un atacante vuelva a reproducir un mensaje de solicitud de licencia y pueda causar un ataque de denegación de servicio (DoS) contra el cliente (Un ataque *denegación de servicio* es un intento de los atacantes de impedir que los usuarios legítimos de un servicio utilicen ese servicio). Por ejemplo, se podría usar un ataque de reproducción utilizando el contador de reversión para &quot;engañar&quot; al servidor de licencias para que piense que el cliente de DRM está revirtiendo su estado, lo que causaría una suspensión de la cuenta.

Para obtener más información sobre la protección de reproducción, consulte `AbstractRequestMessage.getMessageId()` la *Referencia de la API de acceso al Adobe*.
