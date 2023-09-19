---
title: Protección de repetición
description: Protección de repetición
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# Protección de repetición{#replay-protection}

Para la protección de reproducción, puede ser prudente comprobar si el identificador del mensaje se ha visto recientemente llamando a `RequestMessageBase.getMessageId()`. Si es así, un atacante puede estar intentando reproducir la solicitud, lo que debería denegarse. Para detectar intentos de reproducción, el servidor puede almacenar una lista de ID de mensajes vistos recientemente y comprobar cada solicitud entrante en la lista en caché. Para limitar la cantidad de tiempo que se deben almacenar los identificadores de mensajes, llame a `HandlerConfiguration.setTimestampTolerance()`. Si se establece esta propiedad, el SDK denegará cualquier solicitud que lleve una marca de tiempo más allá del número especificado de segundos de tiempo de espera del servidor.
