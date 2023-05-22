---
title: Protección de repetición
description: Protección de repetición
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Protección de repetición{#replay-protection}

Para la protección de reproducción, es posible que desee comprobar si el identificador del mensaje se ha visto recientemente llamando a `RequestMessageBase.getMessageId()`. Si es así, un atacante puede estar intentando reproducir la solicitud, lo que debería denegarse. Para detectar intentos de reproducción, el servidor puede almacenar una lista de ID de mensajes vistos recientemente y comprobar cada solicitud entrante en la lista en caché. Para limitar la cantidad de tiempo que se deben almacenar los identificadores de mensajes, llame a `HandlerConfiguration.setTimestampTolerance()`. Si se establece esta propiedad, el SDK deniega cualquier solicitud que lleve una marca de tiempo durante más del número especificado de segundos fuera del tiempo del servidor.
