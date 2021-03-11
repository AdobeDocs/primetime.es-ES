---
title: Protección contra repetición
description: Protección contra repetición
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Reproducir protección{#replay-protection}

Para la protección de repetición, es posible que desee comprobar si el identificador de mensaje se ha visto recientemente llamando a `RequestMessageBase.getMessageId()`. Si es así, un atacante podría estar intentando reproducir la solicitud, lo que debería ser denegado. Para detectar los intentos de reproducción, el servidor puede almacenar una lista de id de mensajes vistos recientemente y comprobar cada solicitud entrante con la lista en caché. Para limitar la cantidad de tiempo que se deben almacenar los identificadores de mensaje, llame a `HandlerConfiguration.setTimestampTolerance()`. Si se establece esta propiedad, el SDK deniega cualquier solicitud que lleve una marca de tiempo durante más de la cantidad especificada de segundos desde la hora del servidor.
