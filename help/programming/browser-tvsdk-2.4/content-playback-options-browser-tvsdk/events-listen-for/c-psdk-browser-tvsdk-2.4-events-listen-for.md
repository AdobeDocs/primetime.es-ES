---
description: Eventos del TVSDK del explorador indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que empieza a reproducirse o acciones que se producen implícitamente, como la finalización de un anuncio.
seo-description: Eventos del TVSDK del explorador indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que empieza a reproducirse o acciones que se producen implícitamente, como la finalización de un anuncio.
seo-title: Escuchar eventos de Primetime Player
title: Escuchar eventos de Primetime Player
uuid: 7b7c28ac-22ae-46a3-bbeb-bef1b04baeb3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Información general {#listen-for-primetime-player-events-overview}

Eventos del TVSDK del explorador indican el estado del reproductor, los errores que se producen, la finalización de las acciones solicitadas, como un vídeo que empieza a reproducirse o acciones que se producen implícitamente, como la finalización de un anuncio.

Dado que la aplicación debe responder a muchos de estos eventos, debe implementar rutinas de gestión de eventos y registrar estas rutinas con el TVSDK del explorador. Las rutinas llaman a los métodos pertinentes del SDK de TVSDK del explorador para que respondan correctamente.

A continuación se proporciona información adicional sobre los eventos:

* La naturaleza en tiempo real de la reproducción de vídeo requiere una actividad asincrónica (no bloqueante) para muchas operaciones del SDK de TVSDK del explorador.
* El SDK de explorador admite un reproductor de vídeo basado en eventos.

   Proporciona eventos que corresponden a todos los pasos importantes del proceso de reproducción. Los eventos se registran con el mecanismo de eventos de la plataforma y se crean controladores de eventos a los que se llamará cuando se produzcan dichos eventos. *`Event Handlers`* también se conocen como rutinas de llamada de retorno o oyentes de eventos. El SDK TVSDK del explorador proporciona una completa gama de métodos que pueden utilizar los controladores de eventos.
* La aplicación suele iniciar operaciones sin bloqueo, como solicitar que se inicie la reproducción de un vídeo.

   El SDK de TVSDK del explorador se comunica asincrónicamente con la aplicación mediante la distribución de eventos, como cuando se inicia la reproducción del vídeo y un evento cuando finaliza el vídeo. Otros eventos pueden indicar cambios de estado en el reproductor y condiciones de error. Los controladores de eventos realizan las acciones correspondientes.

