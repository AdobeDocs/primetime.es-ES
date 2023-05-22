---
title: Protección de repetición
description: Protección de repetición
copied-description: true
exl-id: dfb6d615-07d2-4303-82cc-10cfee4bb387
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# Protección de repetición{#replay-protection}

Para la protección de reproducción, puede ser prudente comprobar si el identificador del mensaje se ha visto recientemente llamando a `RequestMessageBase.getMessageId()`. Si es así, un atacante puede estar intentando reproducir la solicitud, lo que debería denegarse. Para detectar intentos de reproducción, el servidor puede almacenar una lista de ID de mensajes vistos recientemente y comprobar cada solicitud entrante en la lista en caché. Para limitar la cantidad de tiempo que se deben almacenar los identificadores de mensajes, llame a `HandlerConfiguration.setTimestampTolerance()`. Si se establece esta propiedad, el SDK denegará cualquier solicitud que lleve una marca de tiempo más allá del número especificado de segundos de tiempo de espera del servidor.
