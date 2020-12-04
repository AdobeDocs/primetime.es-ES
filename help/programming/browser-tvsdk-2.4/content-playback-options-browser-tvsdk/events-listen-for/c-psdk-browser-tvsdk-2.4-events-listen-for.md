---
description: Los eventos del TVSDK del explorador indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que empieza a reproducirse o las acciones que se producen implícitamente, como la finalización de un anuncio.
seo-description: Los eventos del TVSDK del explorador indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que empieza a reproducirse o las acciones que se producen implícitamente, como la finalización de un anuncio.
seo-title: Escuchar eventos de Primetime Player
title: Escuchar eventos de Primetime Player
uuid: 7b7c28ac-22ae-46a3-bbeb-bef1b04baeb3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Información general {#listen-for-primetime-player-events-overview}

Los eventos del TVSDK del explorador indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que empieza a reproducirse o las acciones que se producen implícitamente, como la finalización de un anuncio.

Dado que la aplicación debe responder a muchos de estos eventos, debe implementar rutinas de administración de eventos y registrar estas rutinas con el SDK de TVSDK del explorador. Las rutinas llaman a los métodos pertinentes del SDK de TVSDK del explorador para que respondan correctamente.

A continuación se proporciona información adicional sobre eventos:

* La naturaleza en tiempo real de la reproducción de vídeo requiere una actividad asincrónica (sin bloqueo) para muchas operaciones del SDK de TVSDK del explorador.
* El SDK de explorador admite un reproductor de vídeo controlado por evento.

   Proporciona eventos que corresponden a todos los pasos importantes del proceso de reproducción. Los eventos se registran con el mecanismo de evento de la plataforma y se crean controladores de evento a los que se llamará cuando se produzcan esos eventos. *`Event Handlers`* también se conocen como rutinas de llamada de retorno o oyentes de evento. El SDK TVSDK del explorador proporciona una completa gama de métodos que pueden utilizar los controladores de evento.
* La aplicación suele iniciar operaciones de no bloqueo, como solicitar que se reproduzca un inicio de vídeo.

   El SDK de TVSDK del explorador se comunica de forma asincrónica con la aplicación mediante el envío de eventos, como cuando el vídeo inicio de reproducción y un evento cuando termina el vídeo. Otros eventos pueden indicar cambios de estado en el reproductor y condiciones de error. Los controladores de evento realizan las acciones adecuadas.

