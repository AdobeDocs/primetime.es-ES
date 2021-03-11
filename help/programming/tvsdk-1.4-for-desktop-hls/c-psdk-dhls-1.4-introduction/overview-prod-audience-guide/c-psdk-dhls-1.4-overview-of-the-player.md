---
description: 'TVSDK para Desktop HLS incluye una serie de funciones y proporciona las siguientes funciones principales '
title: Funciones de TVSDK de Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Funciones de TVSDK de Primetime{#primetime-tvsdk-features}

TVSDK para Desktop HLS incluye una serie de funciones y proporciona las siguientes capacidades principales:

* Reproducción de VOD y de directo/lineal

   * Administración de la ventana de reproducción, incluidos los métodos que reproducen, detienen, ponen en pausa, buscan y recuperan la posición del cabezal de reproducción.
   * Subtítulos (608, 708, WebVTT) y formas de audio alternativas para aumentar la accesibilidad
   * Control del estilo del texto en los rótulos
   * Capacidad DVR, rebobinado rápido/rápido (modo de reproducción de trucos)
   * Reproducción trucada para contenido en directo y VOD
   * Lógica de velocidad de bits adaptable (ABR) y configuración inicial de los controles ABR
   * Compatibilidad con failover de manifiesto activo
   * Búferes de reproducción ajustables
   * Optimización de redireccionamiento 302
   * Duración del fragmento, tamaño y compatibilidad con seguimiento de tiempo de descarga

* Publicidad

   * VPAID 2.0
   * Vinculación de anuncios del lado del cliente

      * Inserción de publicidad perfecta, incluida la compatibilidad con VAST/VMAP
      * Compatibilidad con etiquetas de referencia personalizadas para anuncios
      * Compatibilidad para marcar, reemplazar y eliminar anuncios C3
      * Flujo de trabajo personalizable de contenido/inserción de publicidad, incluida la señalización de bloqueo

* Protección de contenido

   * Acceso a servicios relacionados con la administración de derechos digitales (DRM)
   * Reproducción de transmisiones HLS sin encriptar o con transmisión en directo HTTP protegida (PHLS)
   * Control de salida basado en resolución, basado en la directiva DRM
   * Compatibilidad con cookies de sesión y cookies de autenticación de medios
   * Paquete de tokens de varios dominios

* Seguimiento de anuncios y vídeos

   * Seguimiento de eventos de QoS
   * Notificaciones que ayudan a TVSDK y a su aplicación a comunicarse de forma asíncrona sobre el estado de los vídeos, anuncios y otros elementos, así como sobre la actividad de registro.
   * Integración con Adobe Analytics y compatibilidad con Heartbeat

* Registro

   * Registro de depuración.
   * Compatibilidad de seguimiento para la duración, el tamaño y el tiempo de descarga del fragmento.