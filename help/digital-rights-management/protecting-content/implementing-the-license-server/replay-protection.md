---
seo-title: Protección contra repetición
title: Protección contra repetición
uuid: c737998a-9c33-48b4-b741-91106697d71f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Protección contra repetición{#replay-protection}

Para proteger la reproducción, es posible que desee comprobar si el identificador de mensaje se ha visto recientemente llamando a `RequestMessageBase.getMessageId()`. Si es así, un atacante podría estar tratando de reproducir la solicitud, lo cual debería ser denegado. Para detectar los intentos de reproducción, el servidor puede almacenar una lista de los identificadores de mensaje vistos recientemente y comprobar cada solicitud entrante en la lista en caché. Para limitar la cantidad de tiempo que deben almacenarse los identificadores de mensaje, llame a `HandlerConfiguration.setTimestampTolerance()`. Si se establece esta propiedad, el SDK deniega toda solicitud que lleve una marca de tiempo durante más de los segundos especificados de la hora del servidor.
