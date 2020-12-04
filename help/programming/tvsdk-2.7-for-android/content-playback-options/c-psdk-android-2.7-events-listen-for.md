---
description: Los eventos de TVSDK indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que empieza a reproducirse o las acciones que se producen implícitamente, como la finalización de un anuncio.
seo-description: Los eventos de TVSDK indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que empieza a reproducirse o las acciones que se producen implícitamente, como la finalización de un anuncio.
seo-title: Escuchar eventos de Primetime Player
title: Escuchar eventos de Primetime Player
uuid: bd0a428c-fa51-41a6-950a-9d6843c6e177
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Información general {#listen-for-primetime-player-events-overview}

Los eventos de TVSDK indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que empieza a reproducirse o las acciones que se producen implícitamente, como la finalización de un anuncio.

Dado que la aplicación debe responder a muchos de estos eventos, debe implementar rutinas de gestión de eventos y registrar estas rutinas con TVSDK. Las rutinas llaman a los métodos pertinentes de TVSDK para que respondan correctamente.

Más información sobre eventos:

* La naturaleza en tiempo real de la reproducción de vídeo requiere una actividad asincrónica (sin bloqueo) para muchas operaciones de TVSDK.
* TVSDK admite un reproductor de vídeo controlado por evento.

   Proporciona eventos que corresponden a todos los pasos importantes del proceso de reproducción. Los eventos se registran con el mecanismo de evento de la plataforma y se crean controladores de evento a los que se llamará cuando se produzcan esos eventos. *`Event Handlers`* también se conocen como rutinas de llamada de retorno o oyentes de evento. TVSDK proporciona una completa gama de métodos que pueden utilizar los controladores de evento.
* La aplicación suele iniciar operaciones de no bloqueo, como solicitar que se reproduzca un inicio de vídeo.

   TVSDK se comunica asincrónicamente con la aplicación mediante el envío de eventos, como cuando el vídeo inicio y un evento cuando termina el vídeo. Otros eventos pueden indicar cambios de estado en el reproductor y condiciones de error. Los controladores de evento realizan las acciones adecuadas.