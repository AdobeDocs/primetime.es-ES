---
description: Los eventos de TVSDK indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que comienza a reproducirse, o las acciones que se producen implícitamente, como la finalización de un anuncio.
title: Escuche los eventos de Primetime Player
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# Información general {#listen-for-primetime-player-events-overview}

Los eventos de TVSDK indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que comienza a reproducirse, o las acciones que se producen implícitamente, como la finalización de un anuncio.

Como la aplicación debe responder a muchos de estos eventos, debe implementar rutinas de gestión de eventos y registrar estas rutinas con TVSDK. Las rutinas llaman a los métodos relevantes de TVSDK para que respondan correctamente.

Más información sobre los eventos:

* La naturaleza en tiempo real de la reproducción de vídeo requiere una actividad asincrónica (sin bloqueo) para muchas operaciones de TVSDK.
* TVSDK admite un reproductor de vídeo impulsado por eventos.

   Proporciona eventos que corresponden a todos los pasos importantes del proceso de reproducción. Los eventos se registran con el mecanismo de eventos de la plataforma y se crean controladores de eventos a los que se llamará cuando se produzcan. *`Event Handlers`* también se conocen como rutinas de rellamada o oyentes de eventos. TVSDK proporciona una completa gama de métodos que pueden utilizar los controladores de eventos.
* Por lo general, la aplicación inicia operaciones sin bloqueo, como solicitar que se inicie la reproducción de un vídeo.

   TVSDK se comunica asincrónicamente con la aplicación mediante el envío de eventos, como cuando el vídeo comienza a reproducirse y un evento cuando termina de reproducirse. Otros eventos pueden indicar cambios de estado en el reproductor y condiciones de error. Los administradores de eventos realizan las acciones adecuadas.