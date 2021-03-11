---
description: TVSDK para Android 3.4 incluye una serie de funciones que puede implementar en sus reproductores.
title: Funciones de TVSDK de Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Funciones de TVSDK de Primetime {#primetime-tvsdk-features}

TVSDK para iOS incluye una serie de funciones que puede implementar en sus reproductores.

Funciones de TVSDK:

* **Reproducción de VOD y de directo/lineal**

   * Administración de la ventana de reproducción, incluidos los métodos que reproducen, detienen, ponen en pausa, buscan y recuperan la posición del cabezal de reproducción
   * Compatibilidad con la reproducción de eventos completos
   * Subtítulos (608, 708, WebVTT) y formas de audio alternativas para aumentar la accesibilidad
   * Controles del estilo del texto en los rótulos
   * Capacidad DVR, avance rápido y rebobinado rápido (los dos últimos se conocen como *modo de reproducción mediante trucos*)
   * Lógica de velocidad de bits adaptable (ABR) y configuración inicial de los controles ABR
   * Compatibilidad con failover de manifiesto activo
   * Búferes de reproducción ajustables
   * Duración del fragmento, tamaño y compatibilidad con seguimiento de tiempo de descarga

* **Publicidad**

   * VPAID 2.0
   * Vinculación de anuncios del lado del cliente

      * Inserción de publicidad perfecta, incluida la compatibilidad con VAST/VMAP
      * Compatibilidad con etiquetas de referencia personalizadas para anuncios
      * Compatibilidad para marcar, reemplazar y eliminar anuncios C3
      * Flujo de trabajo personalizable de contenido/inserción de publicidad, incluida la señalización de bloqueo

* **Protección de contenido**

   * Acceso a servicios relacionados con la administración de derechos digitales (DRM)
   * Reproducción de transmisiones HLS sin encriptar o con transmisión en directo HTTP protegida (PHLS)
   * Control de salida basado en resolución, basado en la directiva DRM

* **Seguimiento de anuncios y vídeos**

   * Seguimiento de eventos de QoS
   * Notificaciones que ayudan a TVSDK y a su aplicación a comunicarse de forma asíncrona sobre el estado de los vídeos, anuncios y otros elementos. Las notificaciones también registran la actividad.

* **Registro**

   * Registro de Debug
   * Compatibilidad de seguimiento para la duración, el tamaño y el tiempo de descarga del fragmento.