---
seo-title: Protección contra repetición
title: Protección contra repetición
uuid: 75f2be65-b2fc-428a-b853-34a4b30960ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Reproducir protección{#replay-protection}

Para proteger la reproducción, puede que sea prudente comprobar si el identificador de mensaje se ha visto recientemente llamando a `RequestMessageBase.getMessageId()`. Si es así, un atacante podría estar tratando de reproducir la solicitud, lo cual debería ser denegado. Para detectar los intentos de reproducción, el servidor puede almacenar una lista de los identificadores de mensaje vistos recientemente y comprobar cada solicitud entrante con la lista en caché. Para limitar la cantidad de tiempo que se deben almacenar los identificadores de mensaje, llame a `HandlerConfiguration.setTimestampTolerance()`. Si se establece esta propiedad, el SDK denegará toda solicitud que lleve una marca de tiempo superior al número especificado de segundos de diferencia en la hora del servidor.
