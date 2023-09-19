---
description: Los eventos de TVSDK indican el estado del reproductor, los errores que se producen, la finalización de las acciones que ha solicitado, como un vídeo que empieza a reproducirse, o las acciones que se producen implícitamente, como la finalización de un anuncio.
title: Escuchar eventos de reproductor de Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Información general {#listen-for-primetime-player-events-overview}

Los eventos de TVSDK indican el estado del reproductor, los errores que se producen, la finalización de las acciones que ha solicitado, como un vídeo que empieza a reproducirse, o las acciones que se producen implícitamente, como la finalización de un anuncio.

Como la aplicación necesita responder a muchos de estos eventos, debe implementar rutinas de control de eventos y registrarlas con TVSDK. Las rutinas llaman a los métodos TVSDK relevantes para responder correctamente.

A continuación se proporciona información adicional sobre los eventos:

* La naturaleza en tiempo real de la reproducción de vídeo requiere una actividad asincrónica (sin bloqueo) para muchas operaciones de TVSDK.
* TVSDK es compatible con un reproductor de vídeo impulsado por eventos.

  Proporciona eventos que corresponden a todos los pasos importantes en el proceso de reproducción. Estos eventos se registran con el mecanismo de eventos de la plataforma y se crean controladores de eventos a los que se llamará cuando se produzcan. *`Event Handlers`* también se conocen como rutinas de devolución de llamada o detectores de eventos. TVSDK proporciona una gama completa de métodos que los controladores de eventos pueden utilizar.
* La aplicación generalmente inicia operaciones sin bloqueo, como solicitar que se inicie la reproducción de un vídeo.

  TVSDK se comunica de forma asíncrona con la aplicación mediante la distribución de eventos, como cuando comienza a reproducirse el vídeo y un evento cuando termina. Otros eventos pueden indicar cambios de estado en el reproductor y condiciones de error. Los controladores de eventos realizan las acciones adecuadas.
