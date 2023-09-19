---
title: Protección de repetición
description: Protección de repetición
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Protección de repetición{#replay-protection}

La protección de reproducción evita que un atacante reproduzca un mensaje de solicitud de licencia y que pueda provocar un ataque de denegación de servicio (DoS) contra el cliente (A *denegación de servicio* ataque es un intento de los atacantes de impedir que los usuarios legítimos de un servicio utilicen ese servicio). Por ejemplo, se podría utilizar un ataque de reproducción con el contador de reversión para &quot;engañar&quot; al servidor de licencias y hacer pensar que el cliente DRM está revirtiendo su estado, lo que provoca una suspensión de la cuenta.

Para obtener más información acerca de la protección de reproducción, consulte `AbstractRequestMessage.getMessageId()` el *Referencia de API de acceso de Adobe*.
